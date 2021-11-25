# linux_make_split_zip_archive_multiple_small_parts_for_AWS

# Making and Restoring a 2 part zip archive 
e.g. for splitting an AWS-Lambda function python env into smaller pieces

https://linuxconfig.org/how-to-split-zip-archive-into-multiple-blocks-of-a-specific-size 

## Make Split Archive Instructions:
1. create an empty parent folder
2. put function.zip into another empty directory in that parent directory
3. unzip the function.zip (in the directory inside the other directory)
4. go back to the parent directory
5. run: 
```
zip -r -s 15m function.zip NAME_OF_DIRECTORY/
```
6. contents of parent directory should now look like this
```
function_old.zip  function.z01  function.z02  function.zip  NAME_OF_DIRECTORY
```

## Restore instructions:
1. put these files
```
function_old.zip  function.z01  function.z02  function.zip
```
into an empty directory
2. run: 
```
zip -F function.zip --out single-function.zip
```
3. remove the 
```
single-function.zip
``` 
 file, rename it as: 
```
function.zip
``` 
 and now it can be uploaded to AWS-Lambda.
