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

## 访问 ODATA 

### http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.xsodata/

``` xml
<service xmlns:atom="http://www.w3.org/2005/Atom" xmlns:app="http://www.w3.org/2007/app" xmlns="http://www.w3.org/2007/app" xml:base="http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.xsodata/">
 <workspace>
    <atom:title>Default</atom:title>
    <collection href="Vehicle">
        <atom:title>Vehicle</atom:title>
    </collection>
    <collection href="Fee">
        <atom:title>Fee</atom:title>
    </collection>
 </workspace>
</service>
```

### ODATA metadata 信息 http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.xsodata/$metadata

``` xml
<edmx:Edmx xmlns:edmx="http://schemas.microsoft.com/ado/2007/06/edmx" Version="1.0">
    <edmx:DataServices xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"     m:DataServiceVersion="2.0">
        <Schema xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices"         xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"        xmlns="http://schemas.microsoft.com/ado/2008/09/edm" Namespace="zhimin.demo.services">
            <EntityType Name="VehicleType">
                <Key>
                    <PropertyRef Name="UID"/>
                </Key>
                <Property Name="UID" Type="Edm.Int32" Nullable="false"/>
                <Property Name="VIN" Type="Edm.String" MaxLength="20"/>
                <Property Name="ENGINE_NO" Type="Edm.String" MaxLength="18"/>
                <Property Name="PLATE_NUMBER" Type="Edm.String" MaxLength="20"/>
                <Property Name="DOC_NUMBER" Type="Edm.String" MaxLength="18"/>
                <Property Name="CARD_ID" Type="Edm.String" MaxLength="18"/>
                <Property Name="MODEL" Type="Edm.String" MaxLength="100"/>
                <Property Name="MAKER" Type="Edm.String" MaxLength="100"/>
                <Property Name="LICENSE_VALID_FROM" Type="Edm.DateTime"/>
                <Property Name="LICENSE_VALID_TO" Type="Edm.DateTime"/>
                <Property Name="OP_CERT_NUMBER" Type="Edm.String" MaxLength="20"/>
                <Property Name="OP_CERT_VALID_FROM" Type="Edm.DateTime"/>
                <Property Name="OP_CERT_VALID_TO" Type="Edm.DateTime"/>
                <Property Name="PURCHASE_DATE" Type="Edm.DateTime"/>
                <Property Name="DELETE_FLAG" Type="Edm.String" DefaultValue="0" MaxLength="1"/>
                <Property Name="EFENCE_FLAG" Type="Edm.String" DefaultValue="0" MaxLength="1"/>
                <NavigationProperty Name="Fee" Relationship="zhimin.demo.services.Vehicle_FeesType"             FromRole="VehiclePrincipal" ToRole="FeeDependent"/>
            </EntityType>
            <EntityType Name="FeeType">
                <Key>
                    <PropertyRef Name="UID"/>
                </Key>
                <Property Name="UID" Type="Edm.String" Nullable="false" MaxLength="32"/>
                <Property Name="REF_VEHICLE.UID" Type="Edm.Int32"/>
                <Property Name="CREATED_ON" Type="Edm.DateTime"/>
                <Property Name="CREATED_BY" Type="Edm.String" MaxLength="50"/>
                <Property Name="CHANGED_ON" Type="Edm.DateTime"/>
                <Property Name="CHANGED_BY" Type="Edm.String" MaxLength="50"/>
                <Property Name="FEE_START_DATE" Type="Edm.DateTime"/>
                <Property Name="FEE_END_DATE" Type="Edm.DateTime"/>
                <Property Name="FEE" Type="Edm.Double"/>
                <Property Name="CURRENCY_CODE" Type="Edm.String" DefaultValue="CNY" MaxLength="3"/>
                <Property Name="DELETE_FLAG" Type="Edm.String" DefaultValue="0" MaxLength="1"/>
            </EntityType>
            <Association Name="Vehicle_FeesType">
                <End Type="zhimin.demo.services.VehicleType" Role="VehiclePrincipal"    Multiplicity="1"/>
                <End Type="zhimin.demo.services.FeeType" Role="FeeDependent" Multiplicity="*"/>
            </Association>
            <EntityContainer Name="demo" m:IsDefaultEntityContainer="true">
                <EntitySet Name="Vehicle" EntityType="zhimin.demo.services.VehicleType"/>
                <EntitySet Name="Fee" EntityType="zhimin.demo.services.FeeType"/>
                <AssociationSet Name="Vehicle_Fees"     Association="zhimin.demo.services.Vehicle_FeesType">
                    <End Role="VehiclePrincipal" EntitySet="Vehicle"/>
                    <End Role="FeeDependent" EntitySet="Fee"/>
                </AssociationSet>
            </EntityContainer>
        </Schema>
    </edmx:DataServices>
</edmx:Edmx>
```


### 查看 Vehicle EntitySet 
http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.xsodata/Vehicle

``` xml
<feed xml:base="http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.xsodata/">
    <title type="text">Vehicle</title>
    <id>
        http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.xsodata/Vehicle
    </id>
    <author>
        <name/>
    </author>
    <link rel="self" title="Vehicle" href="Vehicle"/>
    <entry>
        <id>
            http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.xsodata/Vehicle(10000000)
        </id>
        <title type="text"/>
        <author>
            <name/>
        </author>
        <link rel="edit" title="Vehicle" href="Vehicle(10000000)"/>
        <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/Fee"       type="application/atom+xml;type=feed" title="Fee" href="Vehicle(10000000)/Fee"/>
        <category term="zhimin.demo.services.VehicleType"       scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme"/>
        <content type="application/xml">
            <m:properties>
                <d:UID m:type="Edm.Int32">10000000</d:UID>
                <d:VIN m:type="Edm.String">LFWSRXSJ4KAD14686</d:VIN>
                <d:ENGINE_NO m:type="Edm.String">53170940</d:ENGINE_NO>
                <d:PLATE_NUMBER m:type="Edm.String">豫NR5926</d:PLATE_NUMBER>
                <d:DOC_NUMBER m:type="Edm.String">411401082943</d:DOC_NUMBER>
                <d:CARD_ID m:type="Edm.String">4150028005042</d:CARD_ID>
                <d:MODEL m:type="Edm.String">重型半挂牵引车</d:MODEL>
                <d:MAKER m:type="Edm.String">解放</d:MAKER>
                <d:LICENSE_VALID_FROM       m:type="Edm.DateTime">2019-04-17T00:00:00.0000000</d:LICENSE_VALID_FROM>
                <d:LICENSE_VALID_TO     m:type="Edm.DateTime">2020-04-01T00:00:00.0000000</d:LICENSE_VALID_TO>
                <d:OP_CERT_NUMBER m:type="Edm.String">411406000775</d:OP_CERT_NUMBER>
                <d:OP_CERT_VALID_FROM       m:type="Edm.DateTime">2019-04-22T00:00:00.0000000</d:OP_CERT_VALID_FROM>
                <d:OP_CERT_VALID_TO     m:type="Edm.DateTime">2020-04-30T00:00:00.0000000</d:OP_CERT_VALID_TO>
                <d:PURCHASE_DATE m:type="Edm.DateTime">2019-04-17T00:00:00.0000000</d:PURCHASE_DATE>
                <d:DELETE_FLAG m:type="Edm.String">0</d:DELETE_FLAG>
                <d:EFENCE_FLAG m:type="Edm.String">0</d:EFENCE_FLAG>
            </m:properties>
        </content>
    </entry>
</feed>
```

### 查看具体的 Entity - Vehicle(10000000)
http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.xsodata/Vehicle(10000000)

``` xml
<entry xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom" xml:base="http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.xsodata/">
    <id>
        http://zhiminipmi.z.com:8000/zhimin/demo/services/demo.xsodata/Vehicle(10000000)
    </id>
    <title type="text"/>
    <author>
        <name/>
    </author>
    <link rel="edit" title="Vehicle" href="Vehicle(10000000)"/>
    <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/Fee"       type="application/atom+xml;type=feed" title="Fee" href="Vehicle(10000000)/Fee"/>
    <category term="zhimin.demo.services.VehicleType"       scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme"/>
    <content type="application/xml">
        <m:properties>
            <d:UID m:type="Edm.Int32">10000000</d:UID>
            <d:VIN m:type="Edm.String">LFWSRXSJ4KAD14686</d:VIN>
            <d:ENGINE_NO m:type="Edm.String">53170940</d:ENGINE_NO>
            <d:PLATE_NUMBER m:type="Edm.String">豫NR5926</d:PLATE_NUMBER>
            <d:DOC_NUMBER m:type="Edm.String">411401082943</d:DOC_NUMBER>
            <d:CARD_ID m:type="Edm.String">4150028005042</d:CARD_ID>
            <d:MODEL m:type="Edm.String">重型半挂牵引车</d:MODEL>
            <d:MAKER m:type="Edm.String">解放</d:MAKER>
            <d:LICENSE_VALID_FROM       m:type="Edm.DateTime">2019-04-17T00:00:00.0000000</d:LICENSE_VALID_FROM>
            <d:LICENSE_VALID_TO     m:type="Edm.DateTime">2020-04-01T00:00:00.0000000</d:LICENSE_VALID_TO>
            <d:OP_CERT_NUMBER m:type="Edm.String">411406000775</d:OP_CERT_NUMBER>
            <d:OP_CERT_VALID_FROM       m:type="Edm.DateTime">2019-04-22T00:00:00.0000000</d:OP_CERT_VALID_FROM>
            <d:OP_CERT_VALID_TO     m:type="Edm.DateTime">2020-04-30T00:00:00.0000000</d:OP_CERT_VALID_TO>
            <d:PURCHASE_DATE m:type="Edm.DateTime">2019-04-17T00:00:00.0000000</d:PURCHASE_DATE>
            <d:DELETE_FLAG m:type="Edm.String">0</d:DELETE_FLAG>
            <d:EFENCE_FLAG m:type="Edm.String">0</d:EFENCE_FLAG>
        </m:properties>
    </content>
</entry>
```
