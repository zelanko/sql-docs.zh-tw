---
title: 與順序有關的 Xquery |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- XQuery, sequence
- ordered expressions [XQuery]
ms.assetid: 4f1266c5-93d7-402d-94ed-43f69494c04b
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 978e800ba5539878eb805c16f2460de3761dda59
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38051676"
---
# <a name="xqueries-involving-order"></a>與順序有關的 XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  關聯式資料庫沒有順序的概念。 例如，您不能提出像「從資料庫取得第一個客戶」之類的要求。 不過，您可以在 查詢 XML 文件，並擷取第一個\<客戶 > 項目。 如此一來，您會一直擷取相同客戶。  
  
 此主題依據節點出現在文件中的順序來說明查詢。  
  
## <a name="examples"></a>範例  
  
### <a name="a-retrieve-manufacturing-steps-at-the-second-work-center-location-for-a-product"></a>A. 在產品的第二個工作中心位置擷取製造步驟  
 針對特定產品型號，下列查詢會在製造過程之工作中心位置序列的第二個工作中心位置擷取製造步驟。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    <ManuStep ProdModelID = "{sql:column("Production.ProductModel.ProductModelID")}"  
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
     <Location>  
       { (//AWMI:root/AWMI:Location)[2]/@* }  
       <Steps>  
         { for $s in (//AWMI:root/AWMI:Location)[2]//AWMI:step  
           return  
              <Step>  
               { string($s) }  
              </Step>  
         }  
        </Steps>  
      </Location>  
     </ManuStep>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   大括號括住的運算式由其評估結果取代。 如需詳細資訊，請參閱 < [XML 建構&#40;XQuery&#41;](../xquery/xml-construction-xquery.md)。  
  
-   **@\*** 擷取第二個工作中心位置的所有的屬性。  
  
-   FLWOR 反覆運算 (FOR ...RETURN) 擷取第二個工作中心位置的所有 <`step`> 子元素。  
  
-   [: Column （） 函數 (XQuery)](../xquery/xquery-extension-functions-sql-column.md)正在建構的 XML 中包含的關聯式值。  
  
 以下是結果：  
  
```  
<ManuStep ProdModelID="7" ProductModelName="HL Touring Frame">  
  <Location LocationID="20" SetupHours="0.15"   
              MachineHours="2"  LaborHours="1.75" LotSize="1">  
  <Steps>  
   <Step>Assemble all frame components following blueprint 1299.</Step>  
     …  
  </Steps>  
 </Location>  
</ManuStep>    
```  
  
 上一個查詢只擷取文字節點。 如果您想要將整個 <`step`> 元素傳回相反的移除**string （)** 函式的查詢：  
  
### <a name="b-find-all-the-material-and-tools-used-at-the-second-work-center-location-in-the-manufacturing-of-a-product"></a>B. 在第二個工作中心位置尋找所有用來製造產品的材料和工具  
 針對特定產品型號，下列查詢會在製造過程的工作中心位置順序中，擷取在第二個工作中心位置所使用的工具和材料。  
  
```  
SELECT Instructions.query('  
    declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <Location>  
      { (//AWMI:root/AWMI:Location)[1]/@* }  
       <Tools>  
         { for $s in (//AWMI:root/AWMI:Location)[1]//AWMI:step//AWMI:tool  
           return  
              <Tool>  
                { string($s) }  
              </Tool>  
          }  
        </Tools>  
        <Materials>  
            { for $s in (//AWMI:root/AWMI:Location)[1]//AWMI:step//AWMI:material  
              return  
                 <Material>  
                    { string($s) }  
                 </Material>  
             }  
         </Materials>  
  </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   此查詢會建構 < Loca`tion`> 項目並擷取其屬性值從資料庫。  
  
-   它使用兩個 FLWOR (for...return) 反覆運算：一個擷取工具，另一個擷取使用的材料。  
  
 以下是結果：  
  
```  
<Location LocationID="10" SetupHours=".5"   
          MachineHours="3" LaborHours="2.5" LotSize="100">  
  <Tools>  
    <Tool>T-85A framing tool</Tool>  
    <Tool>Trim Jig TJ-26</Tool>  
    <Tool>router with a carbide tip 15</Tool>  
    <Tool>Forming Tool FT-15</Tool>  
  </Tools>  
  <Materials>  
    <Material>aluminum sheet MS-2341</Material>  
  </Materials>  
</Location>  
```  
  
### <a name="c-retrieve-the-first-two-product-feature-descriptions-from-the-product-catalog"></a>C. 從產品目錄中擷取前兩個產品的功能描述  
 針對特定產品型號，此查詢從產品型號目錄的 <`Features`> 元素中擷取前兩個功能描述。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <ProductModel ProductModelID= "{ data( (/p1:ProductDescription/@ProductModelID)[1] ) }"  
                   ProductModelName = "{ data( (/p1:ProductDescription/@ProductModelName)[1] ) }" >  
       {  
         for $F in /p1:ProductDescription/p1:Features  
         return   
           $F/*[position() <= 2]   
       }  
     </ProductModel>  
      ') as x  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
 查詢主題建構 XML 來包含具有 ProductModelID 和 ProductModelName 屬性的 <`ProductModel`> 元素。  
  
-   此查詢使用 FOR ...RETURN 迴圈來擷取產品型號功能描述。 **Position （)** 函式用來擷取前兩個功能。  
  
 以下是結果：  
  
```  
<ProductModel ProductModelID="19" ProductModelName="Mountain 100">  
 <p1:Warranty   
  xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
  <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
 <p2:Maintenance   
  xmlns:p2="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <p2:NoOfYears>10</p2:NoOfYears>  
  <p2:Description>maintenance contact available through your dealer   
            or any AdventureWorks retail store.  
  </p2:Description>  
 </p2:Maintenance>  
</ProductModel>   
```  
  
### <a name="d-find-the-first-two-tools-used-at-the-first-work-center-location-in-the-manufacturing-process-of-the-product"></a>D. 在產品的製造過程中的第一個工作中心位置尋找所使用的前兩個工具  
 針對產品型號，此查詢會在製造過程的工作中心位置序列的第一個工作中心位置傳回所使用的前兩個工具。 查詢針對製造指示儲存在所指定**指示**資料行**Production.ProductModel**資料表。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   for $Inst in (//AWMI:root/AWMI:Location)[1]  
   return   
     <Location>  
       { $Inst/@* }  
       <Tools>  
         { for $s in ($Inst//AWMI:step//AWMI:tool)[position() <= 2]  
           return  
             <Tool>  
               { string($s) }  
             </Tool>  
         }  
       </Tools>  
     </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 以下是結果：  
  
```  
<Location LocationID="10" SetupHours=".5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
  <Tools>  
    <Tool>T-85A framing tool</Tool>  
    <Tool>Trim Jig TJ-26</Tool>  
  </Tools>  
</Location>   
```  
  
### <a name="e-find-the-last-two-manufacturing-steps-at-the-first-work-center-location-in-the-manufacturing-of-a-specific-product"></a>E. 在特定產品之製造過程的第一個工作中心位置尋找最後兩個製造步驟  
 此查詢會使用**last （)** 函式來擷取最後兩個製造步驟。  
  
```  
SELECT Instructions.query('   
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 以下是結果：  
  
```  
<LastTwoManuSteps>  
   <Last-1Step>When finished, inspect the forms for defects per   
               Inspection Specification .</Last-1Step>  
   <LastStep>Remove the frames from the tool and place them in the   
             Completed or Rejected bin as appropriate.</LastStep>  
</LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML 建構&#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
