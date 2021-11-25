# linux_make_split_zip_archive_multiple_small_parts_for_AWS

# Making and Restoring a 2 part zip archive 
e.g. for splitting an AWS-Lambda function python env into smaller pieces

https://linuxconfig.org/how-to-split-zip-archive-into-multiple-blocks-of-a-specific-size 

## Make Split Archive Instructions:
1. Create an empty parent folder.
2. Put function.zip into another empty directory in that parent directory.
3. Unzip the function.zip (in the directory inside the other directory).
4. Go back to the parent directory.
5. Run: 
```
zip -r -s 15m split_function.zip NAME_OF_DIRECTORY/
```
6. The contents of parent directory should now look like this:
```
split_function.z02        
split_function.z03
split_function.z01  
split_function.zip
```

## Restore instructions:
1. Put these files
```
split_function.z02        
split_function.z03
split_function.z01  
split_function.zip
```
into an empty directory.
2. Run: 
```
zip -F split_function.zip --out function.zip
```
3. This file
```
function.zip
``` 
can now be uploaded to AWS-Lambda.
