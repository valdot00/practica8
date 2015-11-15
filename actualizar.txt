<?php
include("conexion.php");
$con=mysql_query("select * from tablapost");
$reg=mysql_fetch_array($con);
?>

<form action="" method="post">
    <select name="persona">
          <?php
               do{
                   $id=$reg['id'];
                   $titulo=$reg['titulo'];
          ?>
   <option value="<?php echo $id; ?>"><?php echo $titulo; 
                  ?>
   </option>  
          <?php
               }while($reg=mysql_fetch_array($con));
           ?>
    </select>
     <input type="submit" name="actu" value="actualizar"/>   
</form>

<?php
if(isset($_POST['actu'])){
 $p=$_POST['persona'];
 $con1=mysql_query("select *from tablapost where id='$p'")or die(mysql_error());
 $reg1=mysql_fetch_array($con1);

 $t=$reg1['titulo'];
 $c=$reg1['contenido'];

?>
  <form method="post">

    titulo:</br><input name="t" value="<?php echo $t; ?>"/></br> 
    contenido:</br><input name="c" value="<?php echo $c; ?>"/></br>  
  
<input type="hidden" name="id" value="<?php
    echo $p; ?>"/>
<input value="actualizar" type="submit" name="actufinal"/>
  </form>
<?php
}
?>

<?php
if(isset($_POST['actufinal'])){

$id=$_POST['id'];
$t=$_POST['t'];
$c=$_POST['c'];

mysql_query("update tablapost set titulo='$t',contenido='$c' where id='$id'")or die(mysql_error());

echo "<script>alert('datoactu')
location='actualizar.php'</script>";

}
?>