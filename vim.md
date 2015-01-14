
## Key Mappings ##

[Mapping keys in Vim.](http://vim.wikia.com/wiki/Mapping_keys_in_Vim_-_Tutorial_%28Part_1%29)


    :nmap <F2> gUwW
    :nmap <F3> guwW
    
    :map <F4> @q


http://vim.wikia.com/wiki/List_loaded_scripts

## Useful substitues ##

SQL case correction:

    s/\vInsert into (\w+)(\_s*)(\(\_.{-}\))(\_s*)Values(\_s*)(\(\_.{-}\));/INSERT INTO \L\1\2\3\4\EVALUES\5\6;/gi
