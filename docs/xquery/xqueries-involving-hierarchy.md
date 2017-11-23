---
title: "與階層有關的 Xquery |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- hierarchies [XQuery]
- XQuery, hierarchies
ms.assetid: 6953d8b7-bad8-4b64-bf7b-12fa4f10f65c
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e27b8715a426ce4ad2b19fa10a0172a48b8ec67c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="xqueries-involving-hierarchy"></a>與階層有關的 XQuery
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  大部分**xml**類型資料行中的**AdventureWorks**資料庫是半結構化文件。 因此，儲存在每一個資料列中的文件看起來都不同。 此主題的查詢範例說明如何從這些不同的文件中擷取資訊。  
  
## <a name="examples"></a>範例  
  
### <a name="a-from-the-manufacturing-instructions-documents-retrieve-work-center-locations-together-with-the-first-manufacturing-step-at-those-locations"></a>A. 從製造指示文件中，擷取工作中心位置以及這些位置上的第一個製造步驟  
 此查詢會建構 XML 包含產品型號 7 」，如 <`ManuInstr`> 項目，與**ProductModelID**和**ProductModelName**屬性，以及一個或多個 <`Location`>子項目。  
  
 每一個 <`Location`> 元素有它自己的屬性集和一個 <`step`> 子元素。 這個 <`step`> 子元素是工作中心位置的第一個製造步驟。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   \<ManuInstr  ProdModelID = "{sql:column("Production.ProductModel.ProductModelID") }"   
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
            {   
              for $wc in //AWMI:root/AWMI:Location  
              return  
                <Location>  
                 {$wc/@* }  
                 <step1> { string( ($wc//AWMI:step)[1] ) } </step1>  
                </Location>  
            }  
          </ManuInstr>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   **命名空間**關鍵字[XQuery 初構](../xquery/modules-and-prologs-xquery-prolog.md)定義的命名空間前置詞。 稍後在查詢主體中會使用此前置詞。  
  
-   內容切換 Token {) 和 (} 是用來將 XML 建構的查詢切換至查詢評估。  
  
-   **: Column （)**用於所建構的 XML 中包含關聯式值。  
  
-   在建構 <`Location`> 元素時，$wc/@* 會擷取所有工作中心位置屬性。  
  
-   **String （)**函式傳回的字串值從 <`step`> 項目。  
  
 以下是部份結果：  
  
```  
<ManuInstr ProdModelID="7" ProductModelName="HL Touring Frame">  
   <Location LocationID="10" SetupHours="0.5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
     <step1>Insert aluminum sheet MS-2341 into the T-85A   
             framing tool.</step1>  
   </Location>  
   <Location LocationID="20" SetupHours="0.15"   
            MachineHours="2" LaborHours="1.75" LotSize="1">  
      <step1>Assemble all frame components following   
             blueprint 1299.</step1>  
   </Location>  
...  
</ManuInstr>   
```  
  
### <a name="b-find-all-telephone-numbers-in-the-additionalcontactinfo-column"></a>B. 在 AdditionalContactInfo 資料行中尋找所有電話號碼  
 下列查詢利用搜尋 <`telephoneNumber`> 元素的整個階層，來擷取特定客戶連絡人的其他電話號碼。 因為 <`telephoneNumber`> 元素可能出現在階層的任何地方，所以此查詢在搜尋中使用下階和自身運算子 (//)。  
  
```  
SELECT AdditionalContactInfo.query('  
 declare namespace ci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
 declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
for $ph in /ci:AdditionalContactInfo//act:telephoneNumber  
   return  
      $ph/act:number  
') as x  
FROM  Person.Contact  
WHERE ContactID = 1  
```  
  
 以下是結果：  
  
```  
\<act:number   
  xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  112-111-1111  
\</act:number>  
```  
  
 若只要擷取最上層電話號碼，尤其是 <`AdditionalContactInfo`> 的 <`telephoneNumber`> 子元素，則將查詢中的 FOR 運算式變更成  
  
 `for $ph in /ci:AdditionalContactInfo/act:telephoneNumber`。  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 基本概念](../xquery/xquery-basics.md)   
 [XML 建構 &#40;XQuery &#41;](../xquery/xml-construction-xquery.md)   
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
