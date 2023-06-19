---
layout: post
title: Create Google File Dowanload Links in A Different Way
date: 2022-08-25
categories: Eng
tags:
  - HTML+CSS
---

Google Drive is a powerful app to store files of pdf, word, excel and other formats. If you create a copy link from google drive and embed the link into your webpage directly, the default setting is that when user click on the download link, browser will open the file in google doc viewer in a new tab.

It's a handy solution when it comes to pdf files, since you have to view the pdf files any way. But for Word, Excel and other formats, it's sometimes annoying because google doc viewer may not be your first choice app to open and edit files. You have to download the files in google doc viewer window again and then use an other softwares to open them.

The default download link is like this:

`https://docs.google.com/document/d/DOC_FILE_ID/edit...`

<br>

**Solution:**

Replace `/edit` with `/export?format=...`, add the file format that the file should be saved as, then your new download link is ready to go:

```html
https://docs.google.com/document/d/DOC_FILE_ID/export?format=pdf
https://docs.google.com/document/d/DOC_FILE_ID/export?format=doc
```

When users click on the above links, files will be downloaded instead of opened in the new tab viewer. Bravo!

<br>
