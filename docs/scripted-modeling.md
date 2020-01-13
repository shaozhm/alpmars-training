## 创建 ScriptedFee.calculationview 文件

![Scripted Modeling 01](./images/scripted-modeling-01.png)

![Scripted Modeling 02](./images/scripted-modeling-02.png)

![Scripted Modeling 03](./images/scripted-modeling-03.png)

![Scripted Modeling 04](./images/scripted-modeling-04.png)

![Scripted Modeling 05](./images/scripted-modeling-05.png)

![Scripted Modeling 06](./images/scripted-modeling-06.png)

![Scripted Modeling 07](./images/scripted-modeling-07.png)

![Scripted Modeling 08](./images/scripted-modeling-08.png)

![Scripted Modeling 09](./images/scripted-modeling-09.png)

![Scripted Modeling 10](./images/scripted-modeling-10.png)

![Scripted Modeling 11](./images/scripted-modeling-11.png)

![Scripted Modeling 12](./images/scripted-modeling-12.png)

### Scripted SQL
``` sql
 /********* Begin Procedure Script ************/ 
 BEGIN 
 	 var_out = 
 	 SELECT v."UID", v."PLATE_NUMBER", f."FEE"
 	 FROM "zhimin.demo.db::demo.VEHICLE" v
 	 LEFT OUTER JOIN "zhimin.demo.db::demo.FEE" f
 	 ON v."UID" = f."REF_VEHICLE.UID";

END /********* End Procedure Script ************/
```

### 修改 column name

![Scripted Modeling 15](./images/scripted-modeling-15.png)

![Scripted Modeling 16](./images/scripted-modeling-16.png)

![Scripted Modeling 17](./images/scripted-modeling-17.png)

![Scripted Modeling 18](./images/scripted-modeling-18.png)

### Scripted SQL
``` sql
 /********* Begin Procedure Script ************/ 
 BEGIN 
 	 var_out = 
 	 SELECT 
 	 	v."UID" AS "VEHICLE_ID", 
 	 	v."PLATE_NUMBER", 
 	 	f."FEE"
 	 FROM "zhimin.demo.db::demo.VEHICLE" v
 	 LEFT OUTER JOIN "zhimin.demo.db::demo.FEE" f
 	 ON v."UID" = f."REF_VEHICLE.UID";

END /********* End Procedure Script ************/
```

### 修改语意
![Scripted Modeling 19](./images/scripted-modeling-19.png)

### 查看数据

![Scripted Modeling 13](./images/scripted-modeling-13.png)

![Scripted Modeling 14](./images/scripted-modeling-14.png)

## 参考教程
[SAP HANA Scripted Calculation View - Part 1](http://teachmehana.com/sap-hana-scripted-calculation-view-sql/)

[SAP HANA Calculation view using SQL script - Part 2](http://teachmehana.com/sap-hana-calculation-view-using-sql-script/)

[SAP HANA Scripted Calculation View - Part 3](http://teachmehana.com/sap-hana-scripted-calculation-view/)

[SAP HANA Scripted Calculation View](https://blogs.sap.com/2016/09/01/sap-hana-scripted-calculation-view-part-1/)