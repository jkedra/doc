# SVN #
https://help.github.com/categories/writing-on-github/


### Ignoring specific files
    svn propset svn:ignore "*.jpg" . 
    svn propedit svn:ignore . 

### Checkout Selected Dirs only

http://stackoverflow.com/questions/4032059/how-to-checkout-few-files-and-folders-alone-without-checking-out-entire-source

Apart from just checking out the folders you want (which only works if you want the entire subfolder tree as well), Subversion 1.6 supports something referred to as "sparse directories". Basically you can checkout a folder to a certain depth, and then afterwards "drill down" into the folders you are interested in.

Using the command line client, you use the `--depth` and `--set-depth` options to svn update. If you are using TortoiseSVN, there is a "Checkout Depth" option in the checkout dialog.

**EDIT**: To clarify against your specific question, you would first to a checkout of your source tree with depth "immediates". This will give you all your folders, but they will initially be empty. Then you can drill down in the Extensions and Themes directories by updating them to "fully recursive" depth (`svn update --set-depth infinity` or in TortoiseSVN "Update to revision → Update Depth → "Fully Recursive").

**EDIT**: The update depth can be seen as a sort of "visibility level", and is remembered by Subversion, i.e. if you do a svn update on your working copy, it will only update to the current visibility level.

```
svn checkout --immediate http://url
svn update --set-depth immediates Projects
svn update --set-depth infinity FOLDER
```
