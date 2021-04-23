		
<?php

/*

	Author: Amro Eldewiny
	URI: http://arabic-html.com

*/
if(isset($_FILES['image'])){
		$errors= array();
		$file_name = $_FILES['image']['name'];
		$file_size = $_FILES['image']['size'];
		$file_tmp = $_FILES['image']['tmp_name'];
		$file_type = $_FILES['image']['type'];   
		$extension=explode('.',$file_name); 
    	$file_ext=strtolower(end($extension));
		
		$expensions= array("jpeg","jpg","png","gif","pdf","docx"); 		
		if(in_array($file_ext,$expensions) === false){
			$errors[]='<p>لا يمكن رفع هذا الملف</p>';
		}
		if($file_size > 2097152){
		$errors[]='<p>يرجو ان يكون حجم الفايل لا يزيد عن 2 MB</p>';
		}				
		if(empty($errors)){
			if(move_uploaded_file($file_tmp,"images/".$file_name)) {
				echo '<p>تم رفع الملف</p>';
			}
		}else{
			foreach ($errors as $error) {
				echo $error;
			}
		}
	}


?>

<!doctype html>
<html>
	<head>
		<meta charset="utf-8">
		<title>Arabic HTML Files Upload</title>
		<link rel="stylesheet" type="text/css" href="http://yui.yahooapis.com/3.9.0/build/cssreset/cssreset-min.css">
		<link href='http://fonts.googleapis.com/css?family=Lobster' rel='stylesheet' type='text/css'>
		<link rel="stylesheet" type="text/css" href="style.css">	
	</head>

	<body>
		<div class="page">
			<h1>Arabic HTML Files Upload</h1>

			<div class="upload">
				<form action="" method="POST" enctype="multipart/form-data"> 
					<input type="file" class="button" name="image" />
					<input type="submit" class="btn" />
				</form>
			</div>
			
		</div> <!-- End page -->
		<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
	</body>
</html>
