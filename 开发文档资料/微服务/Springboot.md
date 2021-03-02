# SpringBoot （篇）

## 1.Windows 系统发布（jar包）

* 创建文件：xxxxx.bat (创建一个.bat文件。**例如:Battery.bat**)

* 文件内容

  ```java
  @echo off
  set path=C:\Program Files\Java\jdk1.8.0_144\jre\bin
  START "Battery" "%path%\javaw" -jar C:\project\Ba.jar
  ```

  