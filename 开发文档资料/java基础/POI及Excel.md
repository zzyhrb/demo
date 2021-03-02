# 一.了解POI

## 1.POI 讲解

![](F:\gitproject\demo\开发文档资料\images\POI及EXCEL\1.png)



```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>excel</artifactId>
    <version>1.0-SNAPSHOT</version>


    <!--导入依赖-->
    <dependencies>
        <!-- xls(03)-->
        <dependency>
            <groupId>org.apache.poi</groupId>
            <artifactId>poi</artifactId>
            <version>3.9</version>
        </dependency>
        <!--xlsx(07)-->
        <dependency>
            <groupId>org.apache.poi</groupId>
            <artifactId>poi-ooxml</artifactId>
            <version>3.9</version>
        </dependency>
        <!--日期格式化工具-->
        <dependency>
            <groupId>joda-time</groupId>
            <artifactId>joda-time</artifactId>
            <version>2.10.1</version>
        </dependency>

        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>RELEASE</version>
            <scope>compile</scope>
        </dependency>

    </dependencies>



</project>
```



* 03版写入

  ~~~java
  String PATH="F:\\gitproject\\excel\\src";
  @Test
  public void testWrite03() throws Exception {
      //1.创建工作簿
      Workbook workbook =new HSSFWorkbook(); //创建  03版本
      //2.创建一个工作表
      Sheet sheet = workbook.createSheet("观众统计表");
      //3.创建行
      Row row1 = sheet.createRow(0);
      //4 创建一个单元格
      Cell cell= row1.createCell(0);
      cell.setCellValue("今日新增观众");
      //(1,2)
      Cell cell2 = row1.createCell(1);
      cell2.setCellValue(666);
  
      //(2,1)
      Row row2 =sheet.createRow(1);
      Cell cell21 =row2.createCell(0);
      cell21.setCellValue("统计时间");
      //((2,2)
      Cell cell22=row2.createCell(1);
      String time = new DateTime().toString("yyyy-MM-dd HH:mm:ss");
      cell22.setCellValue(time);
  
      //生成一张（IO）03版本使用xls结尾
      FileOutputStream fileOutputStream =new FileOutputStream(PATH+"03测试.xls");
  
      workbook.write(fileOutputStream);
      //关闭流
      fileOutputStream.close();
      System.out.println("生成完毕");
  
  
  
  }
  
  ~~~

* 07版写入

  ~~~ java
  @Test
  public void testWrite07() throws Exception {
      //1.创建工作簿
      Workbook workbook =new XSSFWorkbook();
      //2.创建一个工作表
      Sheet sheet = workbook.createSheet("观众统计表");
      //3.创建行
      Row row1 = sheet.createRow(0);
      //4 创建一个单元格
      Cell cell= row1.createCell(0);
      cell.setCellValue("今日新增观众");
      //(1,2)
      Cell cell2 = row1.createCell(1);
      cell2.setCellValue(666);
  
      //(2,1)
      Row row2 =sheet.createRow(1);
      Cell cell21 =row2.createCell(0);
      cell21.setCellValue("统计时间");
      //((2,2)
      Cell cell22=row2.createCell(1);
      String time = new DateTime().toString("yyyy-MM-dd HH:mm:ss");
      cell22.setCellValue(time);
  
      //生成一张（IO）03版本使用xls结尾
      FileOutputStream fileOutputStream =new FileOutputStream(PATH+"07测试.xlsx");
  
      workbook.write(fileOutputStream);
      //关闭流
      fileOutputStream.close();
      System.out.println("生成完毕");
  
  
  
  }
  
  ~~~

  

 注意: 03 与07 区别 就是对象不同



## 2.POI -Excel 写

* 大文件写HSSF

  > 缺点：对多只能处理65536行，否则会抛出异常。
  >
  > 优点: 过程写入缓存，不操作磁盘，最后一次写入磁盘，速度快。

  ```java
  @Test
  public void testWrite03BigData() throws Exception {
      //时间
      long begin = System.currentTimeMillis();
  
      //创建工作簿
      Workbook workbook =new HSSFWorkbook();
      //创建表
      Sheet sheet = workbook.createSheet();
      //写入数据
      for (int rowNum=0;rowNum<65536;rowNum++){
          Row row = sheet.createRow(rowNum);
          for (int cellNum =0;cellNum<10;cellNum++){
              Cell cell =row.createCell(cellNum);
              cell.setCellValue(cellNum);
          }
      }
      System.out.println("over");
      FileOutputStream outputStream =new FileOutputStream(PATH+"03BigData.xls");
      workbook.write(outputStream);
      outputStream.close();
  
      long end = System.currentTimeMillis();
      System.out.println((double)(end-begin)/1000);
  
  
  }
  
  ```

  

* 大文件写XSSF

  > 缺点：写数据时速度非常慢,非常耗内存，也会发生内存溢出，如100万条
  >
  > 优点：可以写较大的数据量 如20万条。

     

* 大文件SXSSF

  > 优点：可以写非常大的数据量，如100万条甚至更多条，写数据速度快占用更少的内存。



​	







​	

