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
