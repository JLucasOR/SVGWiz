<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-csv/1.0.11/jquery.csv.min.js" integrity="sha512-Y8iWYJDo6HiTo5xtml1g4QqHtl/PO1w+dmUpQfQSOTqKNsMhExfyPN2ncNAe9JuJUSKzwK/b6oaNPop4MXzkwg==" crossorigin="anonymous"></script>

<link rel="stylesheet" href="style.css">

</head> <body> 
<h2>Sample Output</h2>
<div style="margin: auto; width:90%; height: 0; padding-top: 48%; position: relative;"><iframe style=" position: absolute; top: 0; left: 0; width: 100%; height: 100%;" src="Fabaceae_AInteractive.svg" frameborder="0" allowfullscreen></iframe></div>
<h2>Wiz your SVG</h2>
<p> To apply descriptions to an individual svg, prepare a csv with layer names in the first column and descriptions in the second. If you are using an area for your description text outside of your svg, give it the ID [filename]Desc. For Example, a file named Fabaceae_A.svg would require a description area with the ID "Fabaceae_ADesc"</p>
<label for="Upload">Select an SVG</label>
<input accept=".svg" type="file" name="Upload" id="Upload" />
<label for="UpCSV">Add a CSV</label>
<input accept=".csv" type="file" name="UpCSV" id="UpCSV" />
<select name="DescType" id="DescType">
  <option value="Visible">Visible Descriptions</option>
  <option value="Hidden">Screen-reader Only</option>
</select>
<input class="hidden" type="button" id="CSVButton" value="Apply CSV"/>
<input type="button" value="Save" onkeypress="download()" onclick="download()" />
<input type="button" value="Undo" onkeypress="Undo()" onclick="Undo()" />
<input type="button" value="Redo" onkeypress="Redo()" onclick="Redo()" />
<div class="editArea">
<div id="editSidebar" class="editSidebar">
<h3 style="text-align:center">Named Layers</h3>
<ul id="LayerList"></ul>
<input type="button" value="Make Description Area" onkeypress="SetDesc()" onclick="SetDesc()" />
</div>
<div id="imageArea" class="imageArea"></div>
</div>
<div id="DescArea" class="DescArea"></div>
<div id="listArea" class="listArea"></div>

<h2>Help</h2>
<h3>Sample Files</h3>
Download <a href="https://github.com/JLucasOR/SVGWiz/raw/gh-pages/SampleFiles.zip">these sample files</a> and run them through the Wiz above to see it in action. Each image has a paired description csv. Once you have loaded both into the Wiz, you'll see an "apply csv" button, which will pair any descriptions from the csv with the appropriate layers. In the layer panel on the left, select the description area layer and hit the "make description area" button. You can now save the finished svg and open it in any browser.

<h3>SVG Guidelines</h3>
Your SVG should have a some base imagery, which does not change, and multiple feature groups. Each feature group must have a unique layer name and only contain text and focus indicator fills. 
<div class="ExampleArea">
	<div class="ExampleSubarea">
		<figure>
		<img src="https://jlucasor.github.io/SVGWiz/Images/FabaceaeBack.png" alt="Fabaceae vector Background Layers Only" style="width:100%"><figcaption>
			The non-interactive background of the Fabaceae graphic.
		</figcaption>
		</figure>
	</div>
	<div class="ExampleSubarea">
		<figure>
			<img src="https://jlucasor.github.io/SVGWiz/Images/FabaceaeFeatures.png" alt="Fabaceae vector Feature Layers Only" style="width:100%"><figcaption>
			All interactive elements of the Fabaceae graphic, with the background hidden. 
		</figcaption>
		</figure>
	</div>
	<div class="ExampleSubarea">
		<figure>
		<img src="https://jlucasor.github.io/SVGWiz/Images/FabaceaeAll.png" alt="Fabaceae vector All Layers" style="width:100%"><figcaption>
			With all layers visible, the focus indicator for the "Flower" group is selected. This rectangle will have a 0% opacity style on it unless any member of it's group is hovered over, keyboard navigated to, or clicked on. This gives the text itself a larger selection area and allows you to link features within a graphic with it's name in a key.
		</figcaption>
		</figure>
	</div>
</div>

<h3>Preparing a CSV</h3>
CSV stands for Comma Separated Values. The easiest way to produce a CSV is to make a simple table in your favorite spreadsheet software and then export it. 
In Google Sheets, you will find this option under File > Download. 
For SVGWiz to automatically pair your written descriptions to the appropriate layers, the layer name must match the appropriate cell in your table. For an individual image run through the wiz above, you would need a 2 column table with layer names in the first column and descriptions in the second, like the one below. 
<div class="ExampleArea">
	<div class="ExampleSubarea">
		<figure>
		<img src="https://jlucasor.github.io/SVGWiz/Images/FabaceaeLayers.png" alt="Fabaceae vector's Layer List" style="width:100%"><figcaption>
			The layer list of the Fabaceae graphic.
		</figcaption>
		</figure>
	</div>
	<div class="ExampleSubarea">
<table cellspacing="0" cellpadding="0" dir="ltr" border="1">
<tbody>
<tr>
<td>Pinnate</td>
<td>Pea plants typically have pinnately compound leaves.<br /> A compound leaf is one leaf separated into multiple distinct leaflets, these are clear on woody plants as the rachis will be flexible like the stem of the leaf. Compound leaves can also be distinguished by the placement of their stipules - these will only occur at the attachment point of an entire leaf, not that of a leaflet. <br /> Pinnate: Arranged symmetrically on opposite sides of a central axis, similar to a feather. A leaf is odd pinnate when it has one terminal leaf at the end, and even-pinnate otherwise.</td>
</tr>
<tr>
<td>Legume</td>
<td>Plants in the pea family have pea-like fruit, called legumes.</td>
</tr>
<tr>
<td>Keel</td>
<td>The two lower petals of a pea flower, fused at their apex and remaining free at the base, forming a boat-like structure.</td>
</tr>
<tr>
<td>Wing</td>
<td>The petals of a pea flower which surround the keel.</td>
</tr>
<tr>
<td>Banner</td>
<td>The upper petal of a pea flower- a single petal with two lobes though it looks like two that are fused together.</td>
</tr>
<tr>
<td>Flower</td>
<td>The reproductive structure of the plant. Pea flowers are recognizable by their banner, wing, and keel.</td>
</tr>
</tbody>
</table>
</div>
	<div class="ExampleSubarea"><figure>
		<img src="/Images/CSV.png" alt="Google Sheets export menu" style="width:100%"><figcaption>
			How to export a csv from Google Sheets.
		</figcaption></figure>
	</div>
	</div>
<h3>Why is the Layer List Backwards?</h3>
The layers are presented in draw order, which also happens to be tab order for keyboard navigation. This is the opposite of the order you will see them in Illustrator or Inksckape. 
 </body> 


<script type="text/javascript">
var HaveSVG = false;
var HaveCSV = false;
var filename;
var CheckList = [];
var LabelList = [];
var AriaValue = "false";
var ActionHistory = [];
var ActionCount = -1;
document.getElementById('Upload').addEventListener('change', getFile);
document.getElementById('UpCSV').addEventListener('change', getCSV);
document.getElementById('DescType').addEventListener('change', DescToggle);
document.getElementById("CSVButton").addEventListener("click", applyCSV);

function SaveState(){
	ActionCount += 1;
	var data = document.getElementById("imageArea").innerHTML;
	ActionHistory[ActionCount]= data;
	
}

function Undo(){
	ActionCount = ActionCount - 1;
	document.getElementById("imageArea").innerHTML = ActionHistory[ActionCount];
}
function Redo(){
	if (ActionHistory.length > ActionCount){
	ActionCount += 1;
	document.getElementById("imageArea").innerHTML = ActionHistory[ActionCount];}
}


function DescToggle (event) {
	if (document.getElementById("DescType").value = "Hidden"){
		AriaValue = "false"
	}
	else {AriaValue = "true"}
	ToggleArias();
	SaveState();
}

function ToggleArias(){
	var descList = document.getElementsByTagName("desc");
	for (i = 0; i < descList.length; i++) {
		descList[i].setAttribute("aria-hidden", AriaValue);
	}
}
function CheckButton() {
	if (HaveSVG && HaveCSV) {
		let ThatButton = document.getElementById("CSVButton");
		ThatButton.classList.remove("hidden");
	}
}

function getCSV(event) {
	const csvInput = event.target;
	if ('files' in csvInput && csvInput.files.length > 0) {
		placeCSVContent(document.getElementById('listArea'), csvInput.files[0]);
		HaveCSV = true;
		CheckButton();
	}
}

function getFile(event) {
	const input = event.target;
	if ('files' in input && input.files.length > 0) {
		var filepath = document.getElementById('Upload').value;
		var startIndex = (filepath.indexOf('\\') >= 0 ? filepath.lastIndexOf('\\') : filepath.lastIndexOf('/'));
		filename = filepath.substring(startIndex);
		if (filename.indexOf('\\') === 0 || filename.indexOf('/') === 0) {
			filename = filename.substring(1);
		}
		filename = filename.split(".")[0];
		
		var Area = document.getElementById("imageArea");
		placeSVGContent(Area, input.files[0]);
		
	}
}

function addScript(imageArea) {
	let NewScript = document.createElement("script");
	NewScript.setAttribute("type", "text/javascript");
	var ScriptContent = "<![CDATA[function displayDescription(Group) {document.getElementById('" + filename + "Desc').firstChild.data = Group.getElementsByTagName('desc')[0].innerHTML;}]]>";
	NewScript.innerHTML = ScriptContent;
	imageArea.firstChild.appendChild(NewScript);
	document.getElementById("DescArea").setAttribute("ID", filename + "Desc")
	var defzone = document.getElementsByTagName("defs")[0];
	var newStyle = document.createElement("style");
	newStyle.setAttribute("type", "text/css")
	newStyle.innerHTML = ".FeatureGroup :not(text){opacity:0;} *:focus{outline: 0px solid transparent;} .FeatureGroup:hover :not(text){ opacity:0.5;} .FeatureGroup:focus :not(text){opacity:1;} //.Description {font-size: 16px; font-family: OpenSans, Open Sans;}"
	defzone.appendChild(newStyle);
	
}
 function displayDescription(Group) {
        document.getElementById(filename + "Desc").innerHTML = Group.getElementsByTagName('desc')[0].innerHTML;
       }

function placeSVGContent(target, file) {
	readFileContent(file).then(content => {
		target.innerHTML = content;
		getLayers(target);
		addScript(target);
		HaveSVG = true;
		CheckButton();
		SaveState();


	}).catch(error => console.log(error));
}

function placeCSVContent(target, file) {
	readFileContent(file).then(content => {
		target.innerHTML = content;
		HaveCSV = true;
		CheckButton();


	}).catch(error => console.log(error));
}

function readFileContent(file) {
	const reader = new FileReader();
	return new Promise((resolve, reject) => {
		reader.onload = event => resolve(event.target.result);
		reader.onerror = error => reject(error);
		reader.readAsText(file, "windows-1252");
	});
}

function removeAllChildNodes(parent) {
	while (parent.firstChild) {
		parent.removeChild(parent.firstChild);
	}
}
var CheckCount = -1;
const layerList = document.getElementById("LayerList");

function addChildren(Parent, List){
	let layers = Parent.children;
	for (var i = 0; i < layers.length; i++) {
		if (layers[i].id) {
			CheckCount += 1
			let NewLayer = document.createElement("li");
			let LayerBox = document.createElement("input");
			LayerBox.type = "Checkbox";
			LayerBox.id = ("box" + layers[i].id);
			LayerBox.name = ("box" + layers[i].id);
			let LayerLabel = document.createElement("label");
			LayerLabel.setAttribute("for", LayerBox.name);
			LayerLabel.innerHTML = layers[i].id;
			List.appendChild(NewLayer);
			NewLayer.appendChild(LayerBox);
			CheckList[CheckCount] = (LayerBox);
			LabelList[CheckCount] = (LayerLabel);
			NewLayer.appendChild(LayerLabel);
			if (typeof layers[i].firstChild  != "undefined"){
				let NewSublist = document.createElement("ul");
				List.appendChild(NewSublist);
				addChildren(layers[i], NewSublist);}
		}
		
	}
	if (List.children.length  == 0){List.parentNode.removeChild(List);}
}

function getLayers(Image) {
	removeAllChildNodes(layerList);
	CheckList = [];
	LabelList = [];
	var CheckCount = -1;
	addChildren(Image.firstChild, layerList);
}



function download() {
	var data = document.getElementById("imageArea").innerHTML;
	var file = new Blob([data], {
		type: "text"
	});
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

function applyCSV() {
	var Area = document.getElementById("imageArea");
	var features = document.getElementById("listArea").innerHTML;
	var FeatureList = $.csv.toArrays(features);
	var i;
	var ThisLayer;
	var MyDesc;
	for (i = 0; i < FeatureList.length; i++) {
		if (typeof document.getElementById(FeatureList[i][0]) != "undefined"){
			ThisLayer = document.getElementById(FeatureList[i][0]);
			//tabindex='0' onkeypress="displayDescription(this)" onclick="displayDescription(this), focus()" focusable="true" class="FeatureGroup"
			ThisLayer.setAttribute("tabindex","0");
			ThisLayer.setAttribute("onkeypress","displayDescription(this)");
			ThisLayer.setAttribute("onclick","displayDescription(this)");
			ThisLayer.setAttribute("focusable","true");
			ThisLayer.setAttribute("class","FeatureGroup");
			MyDesc = document.createElement("Desc");
			MyDesc.setAttribute("aria-hidden", AriaValue);
			MyDesc.innerHTML = FeatureList[i][1];
			ThisLayer.appendChild(MyDesc);
			
			
		}
	}}
function SetDesc(){
	//find each checked box
	var i
	var AnyCheck = false;
	for (i = 0; i < CheckList.length; i++) {
		if(CheckList[i].checked){	
			AnyCheck = true;
			//find that layer
			var Image = document.getElementById("imageArea");
			var DescLayer = document.getElementById(LabelList[i].innerHTML);
			// set layer id
			//aria-live="assertive" xmlns="http://www.w3.org/1999/xhtml"
			
			var replacement = document.createElementNS('http://www.w3.org/2000/svg',"foreignObject");
			var InnerP = document.createElement("p")
			InnerP.setAttribute("ID",filename + "Desc")
			//<foreignObject id="DescriptionArea" class="cls-203" x="5.57" y="254.29" width="421.71" height="108">
			//<p id="Description" class="Description" aria-live="assertive" xmlns="http://www.w3.org/1999/xhtml"> Select any item in the key for more information.</p>
			//</foreignObject>
			for(var x = 0, l = DescLayer.attributes.length; x < l; ++x){
				var nodeName  = DescLayer.attributes.item(x).nodeName;
				var nodeValue = DescLayer.attributes.item(x).nodeValue;
				replacement.setAttribute(nodeName, nodeValue);
			}
			DescLayer.parentNode.replaceChild(replacement, DescLayer);
			//add wordwrap
			replacement.appendChild(InnerP);
			InnerP.setAttribute("aria-live","assertive")
			InnerP.setAttribute("xmlns","http://www.w3.org/1999/xhtml")
			InnerP.innerHTML = "Select any item for more information."
	}

	}
	if (AnyCheck == false){alert("No layers selected");}
	else{SaveState();}
}






</script>



