# linux_make_split_zip_archive_multiple_small_parts_for_AWS

#### Cheat Sheet
```
Make Splits: zip -r -s 15m function_split.zip *

Rejoin: zip -F function_split.zip --out function.zip

```

## Making and Restoring a 2 part zip archive (from an original zip archive)

e.g. for splitting an AWS-Lambda function python env into smaller pieces

https://linuxconfig.org/how-to-split-zip-archive-into-multiple-blocks-of-a-specific-size 

### These are instructions for taking an already existing function.zip archive (file) and breaking it into smaller files (and then for reassembling them). (These instructions can be modified for use on a unzipped folder as well.) 

## Make Split Archive Instructions:
1. Create an empty parent directory (folder).
2. Put the function.zip into that parent directory.
3. Unzip the function.zip archive (file).
4. Remove the function.zip itself archive from the directory, so that the directory only contains the files (etc) that were inside the function.zip archive.
5. Inside that directory with all the files, run: 
```
zip -r -s 15m function_split.zip *
```
(Note: if you want to zip a directory from the parent directory use:
```
zip -r -s 15m function_split.zip NAME_OF_DIRECTORY/
```
but you do not want that for AWS in this case.)
6. The contents of parent directory should now look like this:
```
function_split.z02        
function_split.z01  
function_split.zip
```

## Restore instructions:
1. Put these files
```
function_split.z02        
function_split.z01  
function_split.zip
```
into an empty directory.
2. Run: 
```
zip -F function_split.zip --out function.zip
```
3. This file
```
function.zip
``` 
can now be uploaded to AWS-Lambda.
