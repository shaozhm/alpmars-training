## 建立文件 demo.xsodata (/zhimin/demo/services/demo.xsodata)
``` js
service namespace "zhimin.demo.services"  { 
   "zhimin.demo.db::demo.VEHICLE" 
   as "Vehicle"
   navigates ("Vehicle_Fees" as "Fee");
   
   "zhimin.demo.db::demo.FEE" as "Fee";
   
   association "Vehicle_Fees" principal "Vehicle"("UID") multiplicity "1" dependent "Fee"("REF_VEHICLE.UID") multiplicity "*"; 
}

settings {
    metadata cache-control "max-age= 604800";
}
```

## 访问 ODATA (http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.xsodata)
