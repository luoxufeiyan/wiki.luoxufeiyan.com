# Migrate to MkDocs


将 Dokuwiki 扩展名改为 markdown

```python
# ref: https://stackoverflow.com/a/37016368/3886059
import os
import sys

directory = os.path.dirname(os.path.realpath(sys.argv[0])) #get the directory of your script
for subdir, dirs, files in os.walk(directory):
 for filename in files:
  if filename.find('.txt') > 0:
   subdirectoryPath = os.path.relpath(subdir, directory) #get the path to your subdirectory
   filePath = os.path.join(subdirectoryPath, filename) #get the path to your file
   newFilePath = filePath.replace(".txt",".md") #create the new name
   os.rename(filePath, newFilePath) #rename your file
```

update img format `![[dir/imgurl.png]]` to markdown format `![]()`

## zh-CN issue

Currently, the MkDocs project did not support Chinese keyword search.

https://github.com/mkdocs/mkdocs/issues/2509#issuecomment-882689383