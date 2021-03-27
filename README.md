
# markdown-pdf export error

The version of Markdown-pdf in vscode is 1.4.4

```
Description,
Using <table> in Markdown to divide the table into columns, an error occurred when exporting the pdf.
```
For example,

```
 <table style="margin-left: auto; margin-right: auto;">
 <tr>
 <td>

 TITLE1|TITLE2
--------|-----
AAAAA | AAAAA
AAAAA | AAAAA
AAAAA | AAAAA
</td>


<td> 

 TITLE1|TITLE2
--------|-----
AAAAA | AAAAA
AAAAA | AAAAA
AAAAA | AAAAA
</td>

</tr>
</table>
```

The display result should be


 <table style="margin-left: auto; margin-right: auto;">
 <tr>
 <td>

 TITLE1|TITLE2
--------|-----
AAAAA | AAAAA
AAAAA | AAAAA
AAAAA | AAAAA
</td>


<td> 

 TITLE1|TITLE2
--------|-----
AAAAA | AAAAA
AAAAA | AAAAA
AAAAA | AAAAA
</td>

</tr>
</table>

But the exported PDF result is,
 TITLE1|TITLE2
--------|-----
AAAAA | AAAAA
AAAAA | AAAAA
AAAAA | AAAAA

&nbsp;

TITLE1|TITLE2
--------|-----
AAAAA | AAAAA
AAAAA | AAAAA
AAAAA | AAAAA

&nbsp;

After a simple analysis,
1. The html format is exported correctly.
2. The _tmp.html file is not exported correctly.
In other words, the results of test.html and test_tmp.html are different.

The temporary solution is,

**Step1.**
Open the extension folder of vscode and find the extension.js file in the Markdown-pdf directory. Use a txt editor to open this file.

**Step2.**
Change two lines of code,
```
const puppeteer = require('puppeteer-core');
// create temporary file
var f = path.parse(filename);
var tmpfilename = path.join(f.dir, f.name + '_tmp.html');
exportHtml(data, tmpfilename);
var options = {
```
==>
```
const puppeteer = require('puppeteer-core');
// create temporary file
var f = path.parse(filename);
var tmpfilename = path.join(f.dir, f.name + '.html');
//exportHtml(data, tmpfilename);
var options = {
```
Save it.

**Step3.**
Restart VSCODE.

**Step4.**
Export HTML and then export PDF.

The principle is that the exported html file is used. The _tmp.html file was discarded.


Markdown-pdf is a very good tool. Do you like it? : )
