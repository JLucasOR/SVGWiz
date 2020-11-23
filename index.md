<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>

<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-csv/1.0.11/jquery.csv.min.js" integrity="sha512-Y8iWYJDo6HiTo5xtml1g4QqHtl/PO1w+dmUpQfQSOTqKNsMhExfyPN2ncNAe9JuJUSKzwK/b6oaNPop4MXzkwg==" crossorigin="anonymous"></script>

<link rel="stylesheet" href="style.css">

</head> <body> 
<h2>Sample Output</h2>
<div style="margin: auto; width:90%; height: 0; padding-top: 48%; position: relative;"><iframe style=" position: absolute; top: 0; left: 0; width: 100%; height: 100%;" src="SVGWizOutput.svg" frameborder="0" allowfullscreen></iframe></div>
<h2>Wiz your SVG</h2>
<p> To apply descriptions to an individual svg, prepare a csv with layer names in the first column and descriptions in the second. If you are using an area for your description text outside of your svg, give it the ID [filename]Desc and the attribute aria-live="assertive". For Example, an input file originally named Fabaceae_A.svg would require a description area with the attributes id="Fabaceae_ADesc" aria-live="assertive". </p>

<div class=Toolbar>
<label for="Upload">Select an SVG</label>
<input accept=".svg" type="file" name="Upload" id="Upload" />
<label for="UpCSV">Add a CSV</label>
<input accept=".csv" type="file" name="UpCSV" id="UpCSV" />
<input class="hidden" type="button" id="CSVButton" value="Apply CSV"/>
<input type="button" value="Save" onkeypress="download()" onclick="download()" />

</div>
<div class=Toolbar> 
<input type="button" value="Undo" onkeypress="Undo()" onclick="Undo()" />
<input type="button" value="Redo" onkeypress="Redo()" onclick="Redo()" />
<select name="DescType" id="DescType">
  <option value="Visible">Visible Descriptions</option>
  <option value="Hidden">Screen-reader Only</option>
</select>
	<label for="DescSizer">Description Font Size:</label>
	<input type="number" id="DescSizer" value="16" style="width:4em;" name="DescSizer">
	<label for="DescSet">Starting Description:</label>
	<input type="text" id="DescSet" value="Select any item for more information." name="DescSet">
</div>
<div class="editArea">

<div id="editSidebar" class="editSidebar">
<h3 style="text-align:center">Named Layers</h3>
<ul id="LayerList"></ul>
<input type="button" value="Make Description Area" onkeypress="SetDesc()" onclick="SetDesc()" /><br>
<input type="button" value="Make Interactive" onkeypress="SetInt()" onclick="SetInt()" /><br>
	<label for="DescSizer">Manual Description:</label><br>
	<input type="text" id="ManDesc" name="ManDesc"><br>
	<input type="button" value="Apply Description" onkeypress="AppDesc()" onclick="AppDesc()" /><br>
	<input type="button" value="Name Group Layers" onkeypress="NameGroups()" onclick="NameGroups()" /><br>
	<input type="button" value="Name Rectangles" onkeypress="NameRects()" onclick="NameRects()" /><br>	
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
	<div class="ExampleSubarea" style="grid-column: 1;">
		<figure>
		<img src="https://jlucasor.github.io/SVGWiz/Images/FabaceaeBack.png" alt="Fabaceae vector Background Layers Only" style="width:95%"><figcaption>
			The non-interactive background of the Fabaceae graphic.
		</figcaption>
		</figure>
	</div>
	<div class="ExampleSubarea" style="grid-column: 2;">
		<figure>
			<img src="https://jlucasor.github.io/SVGWiz/Images/FabaceaeFeatures.png" alt="Fabaceae vector Feature Layers Only" style="width:95%"><figcaption>
			All interactive elements of the Fabaceae graphic, with the background hidden. 
		</figcaption>
		</figure>
	</div>
	<div class="ExampleSubarea" style="grid-column: 3;">
		<figure>
		<img src="https://jlucasor.github.io/SVGWiz/Images/FabaceaeAll.png" alt="Fabaceae vector All Layers" style="width:95%"><figcaption>
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
	<div class="ExampleSubarea" style="grid-column: 1;">
		<figure>
		<img src="https://jlucasor.github.io/SVGWiz/Images/FabaceaeLayers.png" alt="Fabaceae vector's Layer List" style="width:95%"><figcaption>
			The layer list of the Fabaceae graphic.
		</figcaption>
		</figure>
	</div>
	<div class="ExampleSubarea" style="grid-column: 2;">
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
	<div class="ExampleSubarea" style="grid-column: 3;"><figure>
		<img src="https://jlucasor.github.io/SVGWiz/Images/CSV.png" alt="Google Sheets export menu" style="width:95%"><figcaption>
			How to export a csv from Google Sheets.
		</figcaption></figure>
	</div>
	</div>
<h3>Why is the Layer List Backwards?</h3>
The layers are presented in draw order, which also happens to be tab order for keyboard navigation. This is the opposite of the order you will see them in Illustrator or Inkscape. 

<h3>Tool Explanations</h3>
<h4>Visible Descriptions vs Screen-Reader Only</h4>
	This will not visually alter your svg, but toggles the aria-hidden flag on the description elements. You should only switch this if your intention is to have descriptions for screen-reader users which are not printed on the screen. These descriptions will be printed in the space below the image while you are in the editor. 
<h4>Make Description Area</h4>
	Select one of your layers from this list and hit this button to convert it to a description area. At this time, the description area must be a named rectangle. 
<h4>Make Interactive</h4>
	Select one or more of your layers and hit this button to make them keyboard navigable. The layer order as printed on this list will be their tab order.
<h4>Manual Description</h4>
	Use this field and the "apply description" button to manually add a description to any selected layers. This can be used to correct an existing description.
 </body> 


<script type="text/javascript">
var HaveSVG = false;
var HaveCSV = false;
var filename;
var DefDesc = "Select any item for more information.";
var CheckList = [];
var LabelList = [];
var AriaValue = "true";
var ActionHistory = [];
var ActionCount = -1;
document.getElementById('Upload').addEventListener('change', getFile);
document.getElementById('UpCSV').addEventListener('change', getCSV);
document.getElementById('DescType').addEventListener('input', DescToggle);
document.getElementById("CSVButton").addEventListener("click", applyCSV);
document.getElementById('DescSizer').addEventListener('input', DescResize);
document.getElementById('DescSet').addEventListener('input', DescSetter);

function DescSetter(){
	DefDesc = document.getElementById("DescSet").value;
	DescP.innerHTML = DefDesc
	
}
function SaveState(){
	ActionCount += 1;
	var data = document.getElementById("imageArea").innerHTML;
	ActionHistory[ActionCount]= data;
	
}

function Undo(){
	if (ActionCount - 1 > -1){ActionCount = ActionCount - 1;
	document.getElementById("imageArea").innerHTML = ActionHistory[ActionCount];}
}
function Redo(){
	if (ActionHistory.length > ActionCount + 1){
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
var DescArea = document.getElementById("DescArea")
var MyStyle
function addScript(imageArea) {
	let NewScript = document.createElement("script");
	NewScript.setAttribute("type", "text/javascript");
	var ScriptContent = "<![CDATA[function displayDescription(Group) {document.getElementById('" + filename + "Desc').firstChild.data = Group.getElementsByTagName('desc')[0].innerHTML;}]]>";
	NewScript.innerHTML = ScriptContent;
	imageArea.firstChild.appendChild(NewScript);
	DescArea.setAttribute("ID", filename + "Desc")
	var defzone = document.getElementsByTagName("defs")[0];
	MyStyle = document.createElement("style");
	MyStyle.setAttribute("type", "text/css")
	MyStyle.innerHTML = ".FeatureGroup :not(text){opacity:0;} *:focus{outline: 0px solid transparent;} .FeatureGroup:hover :not(text){ opacity:0.5;} .FeatureGroup:focus :not(text){opacity:1;} .Description {font-size: 16px; font-family: OpenSans, Open Sans;}"
	defzone.appendChild(MyStyle);
	
}

function DescResize(event){
	let NewStyle = ".FeatureGroup :not(text){opacity:0;} *:focus{outline: 0px solid transparent;} .FeatureGroup:hover :not(text){ opacity:0.5;} .FeatureGroup:focus :not(text){opacity:1;} .Description {font-size: " + document.getElementById("DescSizer").value + "px; font-family: OpenSans, Open Sans;}";
	MyStyle.innerHTML = NewStyle;
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
		ActionCount = -1;
		ActionHistory = [];
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
var NameCount;
function NameGroups(){
	NameCount = 1;
	NameChildren(document.getElementById("imageArea"),"g");	
	getLayers(document.getElementById("imageArea"));
}
function NameRects(){
	NameCount = 1;
	NameChildren(document.getElementById("imageArea"),"rect");	
	getLayers(document.getElementById("imageArea"));
}
function NameChildren(Layer, Type){
	var Layers = Layer.children;
	for (var i = 0; i < Layers.length; i++) {
		if (Layers[i].tagName == Type){
			Layers[i].setAttribute("id", Type + NameCount);
			NameCount += 1;
		}
		if (Layers[i].children.length > 0){NameChildren(Layers[i],Type);}
	}

	

}

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
	CheckCount = -1;
	addChildren(Image.firstChild, layerList);
}



function download() {
	DescP.innerHTML = DefDesc
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
var DescP;

function SetDesc(){
	//find each checked box
	var AnyCheck = false;
	var MultiCheck = false;
	var Image = document.getElementById("imageArea");
	var DescLayer;
	for (var i = 0; i < CheckList.length; i++) {
		if(CheckList[i].checked){	
			if (AnyCheck == true){MultiCheck = true;}
			AnyCheck = true;
			//find that layer
			DescLayer = document.getElementById(LabelList[i].innerHTML);
			// set layer id
			//aria-live="assertive" xmlns="http://www.w3.org/1999/xhtml"
			if (!(DescLayer.hasAttribute("x"))){
				DescChildren = DescLayer.children;
				if (!(typeof DescChildren[0] == "undefined")){
				for (var x = 0; x < DescChildren.length; x++) {
					if (DescChildren[x].hasAttribute("x")	){
						DescLayer = DescChildren[x];
					}
				}}
			}}
			
	}
	if (MultiCheck == true){alert("Please select only one layer");}
	else if (AnyCheck == false){alert("No layers selected");}
	else if (DescLayer.hasAttribute("x")){
			var replacement = document.createElementNS('http://www.w3.org/2000/svg',"foreignObject");
			DescP = document.createElement("p")
			DescP.setAttribute("ID",filename + "Desc")

			for(var x = 0, l = DescLayer.attributes.length; x < l; ++x){
				var nodeName  = DescLayer.attributes.item(x).nodeName;
				var nodeValue = DescLayer.attributes.item(x).nodeValue;
				replacement.setAttribute(nodeName, nodeValue);
			}
			DescLayer.parentNode.replaceChild(replacement, DescLayer);
			//add wordwrap
			replacement.appendChild(DescP);
			DescP.setAttribute("aria-live","assertive")
			DescP.setAttribute("class","Description")
			DescP.setAttribute("xmlns","http://www.w3.org/1999/xhtml")
			DescP.innerHTML = DefDesc
			SaveState();
			}
	else {alert("Layer is not a rectangle");}
}

function SetInt(){
	//find each checked box
	var AnyCheck = false;
	for (var i = 0; i < CheckList.length; i++) {
		if(CheckList[i].checked){	
			AnyCheck = true;
			var ThisLayer = document.getElementById(LabelList[i].innerHTML);
			ThisLayer.setAttribute("tabindex","0");
			ThisLayer.setAttribute("onkeypress","displayDescription(this)");
			ThisLayer.setAttribute("onclick","displayDescription(this)");
			ThisLayer.setAttribute("focusable","true");
			ThisLayer.setAttribute("class","FeatureGroup");
			
			
			
			}}
		if (AnyCheck == false){alert("No layers selected");}
		else{SaveState();}
}

function AppDesc(){
	//find each checked box
	var AnyCheck = false;
	for (var i = 0; i < CheckList.length; i++) {
		if(CheckList[i].checked){	
			var ThisLayer = document.getElementById(LabelList[i].innerHTML);
			AnyCheck = true;
			var ChildList = ThisLayer.children; 
			var HasDesc = false;
			var MyDesc;
			for (var c = 0; c < ChildList.length; c++){
				if (ChildList[c].tagName == "DESC"){MyDesc = ChildList[c]; HasDesc = true;}
				}
			if (HasDesc == false){	MyDesc= document.createElement("Desc");}
			MyDesc.setAttribute("aria-hidden", AriaValue);
			MyDesc.innerHTML = document.getElementById("ManDesc").value;
			ThisLayer.appendChild(MyDesc);

			
			}}
		if (AnyCheck == false){alert("No layers selected");}
		else{SaveState();}
}		



function ListTemplate(){
	//find each checked box
	var AnyCheck = false;
	for (var i = 0; i < CheckList.length; i++) {
		if(CheckList[i].checked){	
			AnyCheck = true;}}
		if (AnyCheck == false){alert("No layers selected");}
		else{SaveState();}
}			





</script>




