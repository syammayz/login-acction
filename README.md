# login-action
<?php
include 'config.php';

session_start();

$username=$_POST['username'];
$password=$_POST['password'];
echo $password;


$sql="select * from login where username='".$username."' and password='".$password."'";
echo $sql;
$res=mysqli_query($con,$sql);
$data=mysqli_fetch_array($res);
$_SESSION["login_id"]=$data["login_id"];
$_SESSION["username"]=$data["username"];

if ($data['username']== $username && $data['password'] == $password )
{

  if($data['type'] == "admin" && $data['status']=="approved" ) 
  {
  
  	header("location:Admin/index.php");


  }
  elseif($data['type']=="patient"  )
  	{
  	
       	header("location:patient/index.php");
  	}
  	 elseif($data['type']=="lab_technician" )
  	{
  		
       	header("location:technician/index.php");
  	}
  	else
  	{
  		echo"<script>alert('Not approved'); 
	             window.location.href='index.php';</script>";
  	}
}
else
{
	echo"<script>alert('incorrect password'); 
	              window.location.href='login.php';</script>";
}


?>

