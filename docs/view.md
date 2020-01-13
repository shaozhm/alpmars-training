## 创建视图 Fee.hdbview 文件，把表 Fee 中 DELETE_FLAG=1 的数据过滤掉
 
 ``` sql
 --费用视图
 VIEW "FEE_VIEW" AS

 SELECT
     fee."UID", fee."REF_VEHICLE.UID", vehicle."PLATE_NUMBER", fee."CREATED_ON", fee."CREATED_BY", fee."CHANGED_ON", fee."CHANGED_BY", fee."FEE_START_DATE", fee."FEE_END_DATE", fee."FEE", fee."CURRENCY_CODE"
 FROM "DrivingSafety.FEE" AS fee
 LEFT JOIN "DrivingSafety.VEHICLE" AS vehicle ON fee."REF_VEHICLE.UID" = vehicle."UID"
 WHERE fee.DELETE_FLAG=0
 ```
