# Migrate Knowledge to to MkDocs

The knowledge base project has been migrated to MkDocs project, and it works like a charm so far. 

## cons of DokuWiki

The knowledge base project was based on DokuWiki, with a Markdown plugin installed, I wrote wiki pages in Markdown format, and using Doku's media manager to host the attachements. 

However, there always some breaking changes for Doku, and it will get my theme and plugins uncompatable once I upgraded. Moreover, creating or editing wiki is also a tough job, the whole editing process is online, which may cause edit confilcts.

The ideal project structure should be a static site generator which schedully create pages based on the local markdown files. Finally, MkDocs has been adopt to used as the generator.

## MkDocs feature
As its name, MkDocs is a static site generator especially for some project's document, it only use a YAML config file to set up the meta info of the website, followed by a folder which contiain all the markdown files, Mkdocs will automatically create links hierarchylly. It accepts Markdown syntax, so do not need to worry about insert images, just simply put the image file in the directory or subdirectory.

## Migration

Since I alreay use Markdown to write wiki, each file is aleady in Markdown format with a TXT extension name, so what I need to do is to change the extension name to .md for files in each subdirectory, a simple Python script can do this trick.

extensition name from txt to md for each subdirectory.

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

If you insert images in DokuWiki using the GUI panel, the image format should be  `![[dir/imgurl.png]]` , this need to be changed to markdown format `![]()` , a simple Regex could also handle it.

## host on GitHub

I host the knowledge base to a GitHub repo, and implemented a Github Action for CI/CD. It means I can edit the wiki files locally, and when I finish editing, a simple `git push` to push all my local commits to GitHub and CI can automaticlly generate the site and publish to my server.

## issue

The issue of MkDocs are mainly about the `zh-CN` localizations.

Currently, the MkDocs project did not support Chinese keyword search. It works with English keywords, but for Chinese keywords, it returns nothing.

https://github.com/mkdocs/mkdocs/issues/2509#issuecomment-882689383

## other alternatives
If you use Obsidian as your note management tool, you can publish the Obsidian vault to web as a knowledge base, despite the offical publish service, Quartz, is also a good way to publish Obsidian to web.