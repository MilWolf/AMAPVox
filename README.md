# AMAPVox

####Tools to voxelize lidar data.

#####Modules:
<ul>
<li>AMAPVoxGUI : </li><br>
   &emsp; Interface to access to voxelization<br><br>
  
<li>JLas :</li><br>
   &emsp; This is a (las, laz) point reader<br>
   &emsp; @see: [http://www.asprs.org/Committee-General/LASer-LAS-File-Format-Exchange-Activities.html](http://www.asprs.org/Committee-General/LASer-LAS-File-Format-Exchange-Activities.html)<br><br>
  
<li>JRaster</li><br>
   &emsp; Ascii grid file format reader, can retrieve height from x,y position<br><br>

<li>JRiegl</li><br>
   &emsp; Riegl proprietary format reader, read rxp file, use this to get Riegl Terrestrial LIDAR shots and echos + reflectance <br><br>
</ul>
#####Use a module in maven project : <br>

In pom file add repository server:<br><br>

```xml
<repositories>
    <repository>
        <id>github</id>
        <url>https://rawgit.com/MilWolf/AMAPVox/mvn-repo</url>
    </repository>
</repositories>
```
and add module dependency (example for JLas module):

```xml
<dependencies>
    <dependency>
        <groupId>fr.amap.amapvox</groupId>
        <artifactId>JLas</artifactId>
        <version>1.0</version>
    </dependency>
</dependencies>
```

and that's it !

Below an example to read a laz file:

```java
try {
    extractor.openLazFile(new File("C:\\Users\\MilWolf\\Downloads\\file.laz"));
    LasHeader header = extractor.getHeader();
    System.out.println("Points number : " + header.getNumberOfPointrecords());

    Iterator<LasPoint> iterator = extractor.iterator();
    while(iterator.hasNext()){
        LasPoint point = iterator.next();
        System.out.println(point.x + " "+point.y+" "+point.z);
    }
    
}catch (Exception ex) {
    Logger.getLogger(Main.class.getName()).log(Level.SEVERE, null, ex);
}finally{
    extractor.close();
}
```
