---
title: "ParentObject 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ParentObject Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#ParentObject
- http://schemas.microsoft.com/analysisservices/2003/engine#ParentObject
- microsoft.xml.analysis.parentobject
helpviewer_keywords:
- ParentObject element
ms.assetid: f821f8f1-554a-4f16-bf09-262a9448e304
caps.latest.revision: 16
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a03ecf393780d2960e4d5cb4bf3e2ca15c0d997f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="parentobject-element-xmla"></a>ParentObject 元素 (XMLA)
  包含用以建立父代所定義之物件的父物件的識別碼[建立](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Create>  
   ...  
   <ParentObject>  
      <!-- Object reference -->  
   </ParentObject>  
   ...  
</Create>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[建立](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)|  
|子元素|必要的「Analysis Services 指令碼語言」(ASSL) 元素。 指定清單項目指定 ID 的物件，而且其祖系 (但不包括**伺服器**物件。)例如，下列**ParentObject**項目會識別資料分割：<br /><br /> `<ParentObject>`<br /><br /> `<DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>`<br /><br /> `<CubeID>Adventure Works</CubeID>`<br /><br /> `<MeasureGroupID>Internet Sales</MeasureGroupID>`<br /><br /> `<PartitionID>Inernet_Sales_2001</PartitionID>`<br /><br /> `</ParentObject>`|  
  
## <a name="remarks"></a>備註  
 識別碼出現的順序並不重要。  
  
## <a name="example"></a>範例  
 下列範例會建立**購物籃**採礦結構，包含在[!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)]範例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫。  
  
```  
<Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>database</DatabaseID>  
    </ParentObject>  
    <ObjectDefinition>  
        <MiningStructure xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
            <ID>Market Basket</ID>  
            <Name>Market Basket</Name>  
            <Source xsi:type="DataSourceViewBinding">  
                <DataSourceViewID>Adventure Works DW</DataSourceViewID>  
            </Source>  
            <Language>1033</Language>  
            <Collation>Latin1_General_CI_AS</Collation>  
            <Columns>  
                <Column xsi:type="ScalarMiningStructureColumn">  
                    <ID>Order Number</ID>  
                    <Name>Order Number</Name>  
                    <IsKey>true</IsKey>  
                    <Type>Text</Type>  
                    <Content>Key</Content>  
                    <KeyColumns>  
                        <KeyColumn>  
                            <NullProcessing>Error</NullProcessing>  
                            <DataType>WChar</DataType>  
                            <DataSize>20</DataSize>  
                            <Source xsi:type="ColumnBinding">  
                                <TableID>dbo_vAssocSeqOrders</TableID>  
                                <ColumnID>OrderNumber</ColumnID>  
                            </Source>  
                        </KeyColumn>  
                    </KeyColumns>  
                </Column>  
                <Column xsi:type="TableMiningStructureColumn">  
                    <Annotations>  
                        <Annotation>  
                            <Name>MDXFilterComponent</Name>  
                            <Value />  
                        </Annotation>  
                    </Annotations>  
                    <ID>v Assoc Seq Line Items</ID>  
                    <Name>v Assoc Seq Line Items</Name>  
                    <ForeignKeyColumns>  
                        <ForeignKeyColumn>  
                            <NullProcessing>Error</NullProcessing>  
                            <DataType>WChar</DataType>  
                            <DataSize>20</DataSize>  
                            <Source xsi:type="ColumnBinding">  
                                <TableID>dbo_vAssocSeqLineItems</TableID>  
                                <ColumnID>OrderNumber</ColumnID>  
                            </Source>  
                        </ForeignKeyColumn>  
                    </ForeignKeyColumns>  
                    <Columns>  
                        <Column xsi:type="ScalarMiningStructureColumn">  
                            <ID>Model</ID>  
                            <Name>Model</Name>  
                            <IsKey>true</IsKey>  
                            <Type>Text</Type>  
                            <Content>Key</Content>  
                            <KeyColumns>  
                                <KeyColumn>  
                                    <DataType>WChar</DataType>  
                                    <DataSize>50</DataSize>  
                                    <Source xsi:type="ColumnBinding">  
                                        <TableID>dbo_vAssocSeqLineItems</TableID>  
                                        <ColumnID>Model</ColumnID>  
                                    </Source>  
                                </KeyColumn>  
                            </KeyColumns>  
                        </Column>  
                    </Columns>  
                </Column>  
            </Columns>  
            <MiningModels>  
                <MiningModel>  
                    <ID>Market Basket</ID>  
                    <Name>Association</Name>  
                    <Algorithm>Microsoft_Association_Rules</Algorithm>  
                    <AlgorithmParameters>  
                        <AlgorithmParameter>  
                            <Name>MINIMUM_PROBABILITY</Name>  
                            <Value xsi:type="xsd:double">0.1</Value>  
                        </AlgorithmParameter>  
                        <AlgorithmParameter>  
                            <Name>MINIMUM_SUPPORT</Name>  
                            <Value xsi:type="xsd:double">0.01</Value>  
                        </AlgorithmParameter>  
                    </AlgorithmParameters>  
                    <Columns>  
                        <Column>  
                            <ID>Order Number</ID>  
                            <Name>Order Number</Name>  
                            <SourceColumnID>Order Number</SourceColumnID>  
                            <Usage>Key</Usage>  
                        </Column>  
                        <Column>  
                            <ID>v Assoc Seq Line Items</ID>  
                            <Name>v Assoc Seq Line Items</Name>  
                            <SourceColumnID>v Assoc Seq Line Items</SourceColumnID>  
                            <Usage>Predict</Usage>  
                            <Columns>  
                                <Column>  
                                    <ID>Model</ID>  
                                    <Name>Model</Name>  
                                    <SourceColumnID>Model</SourceColumnID>  
                                    <Usage>Key</Usage>  
                                </Column>  
                            </Columns>  
                        </Column>  
                    </Columns>  
                    <Language>1033</Language>  
                    <Collation>Latin1_General_CI_AS</Collation>  
                </MiningModel>  
            </MiningModels>  
        </MiningStructure>  
    </ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

