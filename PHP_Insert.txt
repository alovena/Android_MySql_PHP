<?php
$servername="localhost";
$username="Mysql_ID"; //Mysql 아이디
$password="Mysql_pwd"; //Mysql 비밀번호
$dbname="database_name"; //Db name

$conn =mysqli_connect($servername,$username,$password,$dbname);
mysqli_set_charset($conn,"utf8"); 
if(!$conn){
	die("fail".mysqli_connect_error());
}
	if(($_SERVER['REQUEST_METHOD'] =='POST')){
	$store_name=$_POST['store_name'];
	$user_name=$_POST['user_name'];
	$user_id=$_POST['user_id'];
	$user_pwd=$_POST['user_pwd'];
	$query="insert into Stock_Register(store_name,user_name,user_id,user_pwd) values(?,?,?,?)";
	if($stmt=mysqli_prepare($conn,$query)){
		mysqli_stmt_bind_param($stmt,"ssss",$store_name,$user_name,$user_id,$user_pwd);
		if(mysqli_stmt_execute($stmt)){
			$response = array();
			 $response["success"] = true;
			 echo json_encode($response,JSON_UNESCAPED_UNICODE);
		}
		 
	}

}
?>