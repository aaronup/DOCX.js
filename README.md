DOCX.js
=======

DOCX.js is a JavaScript library for converting the data in binary DOCX files into HTML - and back! Please note that this library is licensed under the Microsoft Office Extensible File License - a license NOT approved by the OSI. While this license is based off of the MS-PL, which is OSI-approved, there are significant differences.

DOCX.js depends on [JSZip](https://github.com/Stuk/jszip)

This fork is modified to accept binary `ArrayBuffer` .docx's, and output `blob` .docx's. It includes support for headers, paragraphs, bold, italics, strikethrough, ordered lists, links (with titles too), inline code, code blocks, block quotes, and limited support for tables.  Works well in combination with markdown, supporting much of what markdown supports.

This fork is not well tested across platforms.  It will not be receiving further updates.  I'll look at pull requests, but you should consider forking instead.

###Create a .docx from a DOM element
`docx.export(domEl, options)`

[See an example in action](https://zerdah.github.io/DOCX.js/).  Click `Download .docx` at the top to download the page.

Example:
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
Memory Leak Warning!  `.href()` creates a `blobURL` that must be later revoked with `docObject.revoke()` or it will stay in memory until the page changes/closes.  Browsers that do not support blobURL's should access the blob directly with `docObject.blob`


###Create a DOM Element from a .docx
`docx.read(arrayBuffer)`

Example:
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
