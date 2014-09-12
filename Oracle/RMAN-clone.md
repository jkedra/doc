[//]: # ( vim:set ts=4: )
# RMAN Clone Example #


Clone may be restored on the same server or a different one.
As long as you don't specify `NOFILENAMECHECK`, your original database
should be - *theoretically* - safe. Nevertheless it is worth considering
to restore the database on a different server.

In the case below the original database is `dev1`, the destination is `tst1`,
and there is RMAN respository database involved as `rman2`.

## Pre-requisites ##

1. Create spfile for the clone database either from the original database pfile or manually.
   Below is the list of parameters you probably have to adjust or check:

	* `remote_login_passwordfile=exclusive` -
	  otherwise you cannot login as SYSDBA to the database.
	* `DB_FILE_NAME_CONVERT  = ('/u08/orafiles/dev1/', '/u08/orafiles/tst1/')` -
	   or specify it in the other way (ex. with DUPLICATE command)
	* `LOG_FILE_NAME_CONVERT = ('/u08/orafiles/dev1/redo/','/u08/orafiles/tst1/redo/')` -
	   the same comment as above.

2. The clone database should be able to be started up remotely by RMAN.
    It means the proper entry is needed in the `listener.ora` file.
    Run `lsnrctl` command and check the location of the `listener.ora` file.
    You will have to add your database entry into the proper listener section:

		SID_LIST_LISTENER =
		  (SID_LIST =
		[...]
		    (SID_DESC =
		      (SID_NAME = tst1)
		      (ORACLE_HOME = /u00/oracle/product/10.2.0.4)
		    )
		[...]

3. Reload listener configuration (`reload`).
4. Create password file or copy it from the other database.
5. Make the final check if you are able to startup database manually from
   `sqlplus sys@tst1 as sysdba`.
   Try in nomount because you probably don't have the controlfile already.
6. Make sure you have enough space to acommodate cloned database.
   It will be exactly the same size as the original one.
7. Optionally, if database has been running already:
	* Clean bdump/cdump/udump directories.
	* Remove all existing clone temp/control/data-files.
8. Optionally create RMAN file with all tasks needed:  
   *file name: aux-tst1.rcv*

		# /u08/orafiles/tst1/
		# /u08/orafiles/tst1/redo`
		# aux: STARTUP FORCE NOMOUNT
		connect target /;
		connect rcvcat rman/****@rman2;
		connect auxiliary sys/****@tst1;
		#startup mount;
		
		RUN {
		   ALLOCATE AUXILIARY CHANNEL aux1 DEVICE TYPE DISK;
		   DUPLICATE TARGET DATABASE TO tst1
		        DB_FILE_NAME_CONVERT=('/u08/orafiles/dev1/','/u08/orafiles/tst1/')
		        LOGFILE
		                '/u08/orafiles/dev1/redo/redo1.log' SIZE 100M,
		                '/u08/orafiles/dev1/redo/redo2.log' SIZE 100M,
		                '/u08/orafiles/dev1/redo/redo3.log' SIZE 100M,
		                '/u08/orafiles/dev1/redo/redo4.log' SIZE 100M
		   ;
		}


> You may specify both DB_FILE_NAME_CONVERT and LOG_FILE_NAME_CONVERT
> in the parameter file instead. It may be more convenient in a case you
> have a lot of logfiles. In such the case it is enough to issue
> `DUPLICATE TARGET DATABASE TO dbname;` without additional options.


## Procedure ##

1. On aux database: startup database as nomount (no controlfile so far):
   `sqlplus sys@tst1 / as sysdba`
2. Target database may be open and running - at least should be mounted
3. Run RMAN and connect databases (steps from the RMAN script above):
	* Connect to target database
	  (here we have ORACLE_SID/HOME set to original db): `connect target /;`.
	* Connect to RC (recovery catalog): `connect rcvcat rman@rman2;`.
    * Connect to aux (clone, already started but not mounted) database:
      `connect auxiliary sys@tst1;`.
	* Run "RUN" block as cited above.

## Further Steps ##

During the `DUPLICATE TARGET DATABASE` command, RMAN restores
the most fresh full or level 0 incremental backup,
applies all incremental backups available and - if database is archive log mode -
applies all archive logs.

For RMAN has no access to online redo logs (the source db is running),
it _opens the database_ with **resetlogs** clause. If the source db was backed up
in a cold way, it won't harm anything. 

Restored database may have the *same db_name* but always have
the **different DBID**. The same DBID is needed only for standby database
and there is a possibility to recreate db with the same DBID.

