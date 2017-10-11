# image-downloader
download batch images from shopify server
<?php
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "wazoimages";
 
// 创建连接
$conn = new mysqli($servername, $username, $password, $dbname);
// Check connection
if ($conn->connect_error) {
    die("connect error: " . $conn->connect_error);
} 
 
$sql = "SELECT id, url FROM wazoimages";
$result = $conn->query($sql);
 
if ($result->num_rows > 0) {

function GrabImage($url,$filename="") {
   if($url==""):return false;endif;
   $fileArr = pathinfo($url); 
$filename=$fileArr['basename'];
   ob_start();
   readfile($url);
   $img = ob_get_contents();
   ob_end_clean();
   $size = strlen($img);

   $fp2=@fopen($filename, "a");
   fwrite($fp2,$img);
   fclose($fp2);

   return $filename;
}
    // 输出数据
    while($row = $result->fetch_assoc()) {
        echo "id: " . $row["id"]. " - URL: " . $row["url"]. " <br>";
     GrabImage($row["url"],"");
}
}

$conn->close();
?>
