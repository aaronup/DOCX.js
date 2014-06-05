DOCX.js
=======

DOCX.js is a JavaScript library for converting the data in base64 DOCX files into HTML - and back! Please note that this library is licensed under the Microsoft Office Extensible File License - a license NOT approved by the OSI. While this license is based off of the MS-PL, which is OSI-approved, there are significant differences.

This fork is modified to accept binary ArrayBuffer .docx's, and output blob .docx's

###Create a .docx from a DOM element

```javascript
var docDOM = document.getElementById('example');
var docObject = docx.export(docDOM, // required DOM Object
{
	creator: "Creator", // optional String
	lastModifiedBy: "Last person to modify", // optional String
	created: new Date(), // optional Date Object
	modified: new Date() // optional Date Object
});
var link = document.createElement('a');
link.appendChild(document.createTextNode("Download Link Text"));
link.title = "Download Title";
link.download = "FilenameHere.docx";
link.href = docObject.href();
document.getElementById("example").appendChild(link);
```
Note this creates a `blobURL` that must be later revoked: `docObject.revoke()`


###Create a DOM Element from a .docx

```javascript
document.getElementById('files').addEventListener('change', function(e){
var reader = new FileReader();
	reader.onload = function(ev) {
		var docObject = docx.read(ev.target.result); // accepts ArrayBuffers
		document.getElementById("center").appendChild(docObject.DOM);
	};
	reader.readAsArrayBuffer(e.target.files[0]);
}, false);
```
