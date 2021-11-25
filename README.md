# linux_make_split_zip_archive_multiple_small_parts_for_AWS
## Making and Restoring a 2 part zip archive 
e.g. for splitting an AWS-Lambda function python env into smaller pieces

https://linuxconfig.org/how-to-split-zip-archive-into-multiple-blocks-of-a-specific-size 

## Make Split Archive Instructions:
1. Create an empty parent folder.
2. Put function.zip into another empty directory in that parent directory.
3. Unzip the function.zip (in the directory inside the other directory).
4. Go back to the parent directory.
5. Run: 
```
zip -r -s 15m function.zip NAME_OF_DIRECTORY/
```
6. The contents of parent directory should now look like this:
```
function_old.zip  function.z01  function.z02  function.zip  NAME_OF_DIRECTORY
```

## Restore instructions:
1. Put these files
```
function_old.zip  function.z01  function.z02  function.zip
```
into an empty directory.
2. Run: 
```
zip -F function.zip --out single-function.zip
```
3. Remove the 
```
single-function.zip
``` 
 file.

4. Rename it as: 
```
function.zip
``` 
 and now it can be uploaded to AWS-Lambda.
