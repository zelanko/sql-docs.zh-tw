---
title: 與階層有關的 Xquery |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- hierarchies [XQuery]
- XQuery, hierarchies
ms.assetid: 6953d8b7-bad8-4b64-bf7b-12fa4f10f65c
author: rothja
ms.author: jroth
ms.openlocfilehash: 8aa762af8e08c72f7f00369219771c371ce39aac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946109"
---
# <a name="xqueries-involving-hierarchy"></a>與階層有關的 XQuery
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  大部分**xml**類型資料行中的**AdventureWorks**資料庫是半結構化文件。 因此，儲存在每一個資料列中的文件看起來都不同。 此主題的查詢範例說明如何從這些不同的文件中擷取資訊。  
  
## <a name="examples"></a>範例  
  
### <a name="a-from-the-manufacturing-instructions-documents-retrieve-work-center-locations-together-with-the-first-manufacturing-step-at-those-locations"></a>A. 從製造指示文件中，擷取工作中心位置以及這些位置上的第一個製造步驟  
 對於 產品型號 7 」，此查詢會建構 XML 包含 <`ManuInstr`> 項目，與**ProductModelID**並**ProductModelName**屬性，以及一個或多個 <`Location`>子項目。  
  
 每個 <`Location`> 項目有自己的屬性和一個 <`step`> 子元素。 這個 <`step`> 子元素是工作中心位置的第一個製造步驟。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
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
  
-   **命名空間**中的關鍵字[XQuery 初構](../xquery/modules-and-prologs-xquery-prolog.md)定義的命名空間前置詞。 稍後在查詢主體中會使用此前置詞。  
  
-   內容切換 Token {) 和 (} 是用來將 XML 建構的查詢切換至查詢評估。  
  
-   **: Column （)** 用來包含所建構的 XML 中的關聯式值。  
  
-   在建構 <`Location`> 項目，$wc/@* 擷取所有工作中心位置屬性。  
  
-   **String （)** 函式傳回的字串值從 <`step`> 項目。  
  
 以下是部份結果：  
  
```xml
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
 下列查詢會搜尋整個階層，來擷取特定客戶連絡人的其他電話號碼 <`telephoneNumber`> 項目。 因為 <`telephoneNumber`> 項目可以出現在任何位置的階層，此查詢使用階和自身運算子 (/ /) 在搜尋。  
  
```sql
SELECT AdditionalContactInfo.query('  
 declare namespace ci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
 declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
for $ph in /ci:AdditionalContactInfo//act:telephoneNumber  
   return  
      $ph/act:number  
') as x  
FROM  Person.Contact  
WHERE ContactID = 1  
```  
  
 以下是結果：  
  
```xml
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  111-111-1111  
\</act:number>  
\<act:number   
  xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  112-111-1111  
\</act:number>  
```  
  
 若要擷取只有最上層的電話號碼，尤其是 <`telephoneNumber`> 子元素 <`AdditionalContactInfo`>，在查詢中的 FOR 運算式變更為  
  
 `for $ph in /ci:AdditionalContactInfo/act:telephoneNumber`.  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 基本概念](../xquery/xquery-basics.md)   
 [XML 建構&#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
