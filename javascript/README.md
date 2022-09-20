# Javascript

## 跨網域讀JS
```
<script crossorigin src="..."></script>
```

## Get URL params
```
var url_string = window.location;
var url = new URL(url_string);
var c = url.searchParams.get("c");
```

## Modify history params
```
window.history.replaceState({}, document.title, "?search=" + XXXX);
```

## Get client language
```
window.navigator.language
```

## file upload replace image tag, javascript FileReader
```
<img id="imageTag">
<input type="file" onchange="replaceImage(this)">

function replaceImage(input, i) {
	if (input.files && input.files[0]) {
		var reader = new FileReader();
		reader.onload = function (e) {
			var imageShowId = '#imageTag';
			$(imageShowId).attr('src', e.target.result);
		};
		reader.readAsDataURL(input.files[0]);
	}
}
```

## fileupload input Clear
```
var fileTag = document.getElementById(inputId);
document.getElementById(inputId).outerHTML = fileTag.outerHTML;
```

## javascript form
```
var f = document.createElement("form");
f.setAttribute('target',"_blank");
f.setAttribute('method',"get");
f.setAttribute('action',"/url");
document.body.appendChild(f);

var obj = document.createElement("input");
obj.type = "hidden";
obj.name = "inputName";
obj.value = inputValue;
f.appendChild(obj);
f.submit();
```

## Get element methods
```
document.getElementById("myId");
document.getElementsByTagName("p");
document.getElementsByClassName("myClass");
document.querySelectorAll("p.myId");
document.getElementsByName("myName");
```

## Drag
js
```
# javascript:

function Position(x, y) {
	this.X = x ? x : 0;
	this.Y = y ? y : 0;
	this.add = function (val) {
		if (val) {
			if (!isNaN(val.X)) this.X += val.X;
			if (!isNaN(val.Y)) this.Y += val.Y;
		}
		return this;
	};
	this.subtract = function (val) {
		if (val) {
			if (!isNaN(val.X)) this.X -= val.X;
			if (!isNaN(val.Y)) this.Y -= val.Y;
		}
		return this;
	};
	this.min = function (val) {
		if (!val) return this;
			if (!isNaN(val.X)) this.X = Math.min(this.X, val.X);
			if (!isNaN(val.Y)) this.Y = Math.min(this.Y, val.Y);
		return this;
	};
	this.max = function (val) {
		if (!val) return this;
		if (!isNaN(val.X)) this.X = Math.max(this.X, val.X);
		if (!isNaN(val.Y)) this.Y = Math.max(this.Y, val.Y);
		return this;
	};
	this.apply = function (element, control) {
		if (!element) return;
		if (!isNaN(this.X)) {
			if (control && (control.orientation != 'horizontal' || this.X > control.upperLimit || this.X < control.lowerLimit)) return;
			element.style.left = this.X + 'px';
		}
		if (!isNaN(this.Y)) {
			if (control && (control.orientation != 'vertical' || this.Y > control.upperLimit || this.Y < control.lowerLimit)) return;
			element.style.top = this.Y + 'px';
		}
	};
}
function absoluteCursorPosition(e) {
	e = e || window.event;
	if (isNaN(window.scrollX)) return new Position(e.clientX + document.documentElement.scrollLeft + document.body.scrollLeft,
	e.clientY + document.documentElement.scrollTop + document.body.scrollTop);
	else return new Position(e.clientX + window.scrollX, e.clientY + window.scrollY);
}
function dragObject(element, startCallback, moveCallback, endCallback) {
	if (!element) return;
	var cursorStartPos = null;
	var elementStartPos = null;
	var dragging = false;
	var control;
	if (document.addEventListener) element.addEventListener("mousedown", dragStart, false);
	else element.attachEvent("onmousedown", dragStart);
	function dragStart(e) {
		e = e || window.event;
		if ((e.which && e.which != 1) || (e.button && e.button != 1)) return; //only allow mouse left key
		if (dragging) return;
		dragging = true;
		if (startCallback) control = startCallback(e, element);
		cursorStartPos = absoluteCursorPosition(e);
		elementStartPos = new Position(parseInt(element.style.left), parseInt(element.style.top));
		if (document.addEventListener) {
			document.addEventListener("mousemove", dragGo, false);
			document.addEventListener("mouseup", dragStop, false);
		} else {
			document.attachEvent("onmousemove", dragGo);
			document.attachEvent("onmouseup", dragStop);
		}
	}
	function dragGo(e) {
		if (!dragging) return;
		var newPos = absoluteCursorPosition(e).add(elementStartPos).subtract(cursorStartPos);
		newPos.apply(element, control);
		if (moveCallback) moveCallback(e, element, newPos);
	}
	function dragStop(e) {
		if (!dragging) return;
		dragging = false;
		cursorStartPos = null;
		elementStartPos = null;
		if (endCallback) endCallback(e, element);
		if (document.removeEventListener) {
			document.removeEventListener("mousemove", dragGo, false);
			document.removeEventListener("mouseup", dragStop, false);
		} else {
			document.detachEvent("onmousemove", dragGo);
			document.detachEvent("onmouseup", dragStop);
		}
	}
	this.dispose = function () {
		if (element.removeEventListener) element.removeEventListener("mousedown", dragStart, false);
		else element.detachEvent("onmousedown", dragStart);
	};
}
```
html
```
# html

<script> var dothis = new dragObject(document.getElementById("demoimage"));</script>
<span style="background-color:green;position:relative;width:100px;cursor:move;color:white;" id="demoimage">test</span>
```

## 有些網頁會用js去鎖定右鍵，要把它unlock
```
javascript:(function() { function R(a){ona = "on"+a; if(window.addEventListener) window.addEventListener(a, function (e) { for(var n=e.originalTarget; n; n=n.parentNode) n[ona]=null; }, true); window[ona]=null; document[ona]=null; if(document.body) document.body[ona]=null; } R("contextmenu"); R("click"); R("mousedown"); R("mouseup"); R("selectstart");})()
```

## listen file change by javascript
```
<!DOCTYPE HTML>
<html>
<head>
	<meta http-equiv="Content-type" content="text/html;charset=UTF-8">
	<title>Watch for a file change</title>
	<style type='text/css'>
		body {
			font-family: sans-serif;
		}
	</style>
</head>
<body>
<input type='file' id='filename'>
<input type='button' id='btnStart' value='Start'>
<script type='text/javascript'>
(function() {
	var input;
	var lastMod;

	document.getElementById('btnStart').onclick = function() {
		startWatching();
	};
	function startWatching() {
		var file;

		if (typeof window.FileReader !== 'function') {
			display("The file API isn't supported on this browser yet.");
			return;
		}

		input = document.getElementById('filename');
		if (!input) {
			display("Um, couldn't find the filename element.");
		}
		else if (!input.files) {
			display("This browser doesn't seem to support the `files` property of file inputs.");
		}
		else if (!input.files[0]) {
			display("Please select a file before clicking 'Show Size'");
		}
		else {
			file = input.files[0];
			lastMod = file.lastModifiedDate;
			display("Last modified date: " + lastMod);
			display("Change the file");
			setInterval(tick, 250);
		}
	}

	function tick() {
		var file = input.files && input.files[0];
		if (file && lastMod && file.lastModifiedDate.getTime() !== lastMod.getTime()) {
			lastMod = file.lastModifiedDate;
			display("File changed: " + lastMod);
		}
	}

	function display(msg) {
		var p = document.createElement('p');
		p.innerHTML = msg;
		document.body.appendChild(p);
	}
})();
</script>
</body>
</html>
```
