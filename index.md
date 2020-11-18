<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<link rel="stylesheet" href="style.css">

</head> <body> 
<h2>Sample Output</h2>
<div style="margin: auto; width:90%; height: 0; padding-top: 48%; position: relative;"><iframe style=" position: absolute; top: 0; left: 0; width: 100%; height: 100%;" src="Fabaceae_AInteractive.svg" frameborder="0" allowfullscreen></iframe></div>

<input accept=".svg" type="file" name="Upload" id="Upload" />
<input type="button" value="Save" onkeypress="download()" onclick="download()" />
<div class="editArea">
<div id="editSidebar" class="editSidebar">
<h3 style="text-align:center">Named Layers</h3>
<ul id="LayerList"></ul>
</div>
<div id="imageArea" class="imageArea"></div>
</div>


 </body> 


<script type="text/javascript">
document.getElementById('Upload')
  .addEventListener('change', getFile)

function getFile(event) {
	const input = event.target
  if ('files' in input && input.files.length > 0) {
	  placeFileContent(
      document.getElementById('imageArea'),
      input.files[0])
  }
}

function placeFileContent(target, file) {
	readFileContent(file).then(content => {
  	target.innerHTML = content
	getLayers(target)
  }).catch(error => console.log(error))
}

function readFileContent(file) {
	const reader = new FileReader()
  return new Promise((resolve, reject) => {
    reader.onload = event => resolve(event.target.result)
    reader.onerror = error => reject(error)
    reader.readAsText(file, "windows-1252")
  })
}
function removeAllChildNodes(parent) {
    while (parent.firstChild) {
        parent.removeChild(parent.firstChild);
    }
}
function getLayers(Image){
	let layers = Image.getElementsByTagName("g");
	const layerList = document.getElementById("LayerList");
	removeAllChildNodes(LayerList);
	var i;
	for (i = 0; i < layers.length; i++) {
		if (layers[i].id){
			let NewLayer = document.createElement("li");
			let LayerBox = document.createElement("input");
			LayerBox.type = "Checkbox";
			LayerBox.id=("box" + layers[i].id);
			LayerBox.name=("box" + layers[i].id);
			let LayerLabel = document.createElement("label");
			LayerLabel.setAttribute("for",LayerBox.name);
			LayerLabel.innerHTML = layers[i].id;
			layerList.appendChild(NewLayer)
			NewLayer.appendChild(LayerBox)
			NewLayer.appendChild(LayerLabel)}
	}
}


function download() {
    var data = document.getElementById("imageArea").innerHTML
	var file = new Blob([data], {type: "text"});
    if (window.navigator.msSaveOrOpenBlob) // IE10+
        window.navigator.msSaveOrOpenBlob(file, "SVGWizOutput.svg");
    else { // Others
        var a = document.createElement("a"),
                url = URL.createObjectURL(file);
        a.href = url;
        a.download = "SVGWizOutput.svg";
        document.body.appendChild(a);
        a.click();
        setTimeout(function() {
            document.body.removeChild(a);
            window.URL.revokeObjectURL(url);  
        }, 0); 
    }
}
</script>
