# Jsonp

## Jsonp
```
$.ajax({
    url: "URL.html",
    dataType: 'jsonp', //data type必須設定成 'jsonp'
    crossDomain: true,
    data: data,
    success: callback,
    error: callback
});
```

## Ajax upload file
```
var files;
$('input[type=file]').on('change', prepareUpload);
function prepareUpload(event){
	files = event.target.files;
}

$('form').on('submit', uploadFiles);
function uploadFiles(event) {
	event.stopPropagation();
	event.preventDefault();
	var data = new FormData();
	$.each(files, function(key, value) {
		data.append(key, value);
	});
	$.ajax({
		url: 'submit.php',
		type: 'POST',
		data: data,
		cache: false,
		dataType: 'json',
		processData: false,
		contentType: false,
		success: function(data, textStatus, jqXHR) {
			if(typeof data.error === 'undefined') {
				submitForm(event, data);
			}
			else {
				console.log('ERRORS: ' + data.error);
			}
		},
		error: function(jqXHR, textStatus, errorThrown) {
			console.log('ERRORS: ' + textStatus);
		}
	});
}

$data = array();
if(isset($_GET['files'])) {
	$error = false;
	$files = array();
	$uploaddir = './uploads/';
	foreach($_FILES as $file)
	{
		if(move_uploaded_file($file['tmp_name'], $uploaddir .basename($file['name'])))
		{
			$files[] = $uploaddir .$file['name'];
		}
		else
		{
			$error = true;
		}
	}
	$data = ($error) ? array('error' => 'There was an error uploading your files') : array('files' => $files);
}
else {
	$data = array('success' => 'Form was submitted', 'formData' => $_POST);
}

function submitForm(event, data) {
	$form = $(event.target);
	var formData = $form.serialize();
	$.each(data.files, function(key, value) {
		formData = formData + '&filenames[]=' + value;
	});
	$.ajax({
		url: 'submit.php',
		type: 'POST',
		data: formData,
		cache: false,
		dataType: 'json',
		success: function(data, textStatus, jqXHR) {
			if(typeof data.error === 'undefined') {
				console.log('SUCCESS: ' + data.success);
			}
			else {
				console.log('ERRORS: ' + data.error);
			}
		},
		error: function(jqXHR, textStatus, errorThrown) {
			// Handle errors here
			console.log('ERRORS: ' + textStatus);
		},
		complete: function() {
			// STOP LOADING SPINNER
		}
	});
}
```

## checkbox get value
```
$('input:checkbox:checked[name="target_ids[]"]').map(function() { return $(this).val(); }).get();

# get by name and check
$( "input[name='target_names[257][]']:checked:enabled" )
```

## select get value or text
```
$('#select_exception_template').find(':selected').text()
$('#select_exception_template').find(':selected').val()
```
