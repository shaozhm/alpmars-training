## 暴露 ODATA 

``` js
service namespace "zhimin.demo.services"  { 
    "zhimin.demo.models/Fee.calculationview" as "FeeSummary" keys ("VEHICLE_ID");
}
```

## 查看数据

``` xml
<feed xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom" xml:base="http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.xsodata/">
    <title type="text">FeeSummary</title>
    <id>http://zhiminipmi.z.com:8000/zhimin/demo/services/demo. xsodata/FeeSummary</id>
    <author>
        <name />
    </author>
    <link rel="self" title="FeeSummary" href="FeeSummary" />
    <entry>
        <id>http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.     xsodata/FeeSummary(10000000)</id>
        <title type="text" />
        <author>
            <name />
        </author>
        <link rel="edit" title="FeeSummary" href="FeeSummary(10000000)" />
        <category term="zhimin.demo.services.FeeSummaryType"        scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
        <content type="application/xml">
            <m:properties>
                <d:VEHICLE_ID m:type="Edm.Int32">10000000</d:VEHICLE_ID>
                <d:PLATE_NUMBER m:type="Edm.String">豫NR5926</d:PLATE_NUMBER>
                <d:FEE m:type="Edm.Double">720.5</d:FEE>
            </m:properties>
        </content>
    </entry>
</feed>
```