---
title: 涉及階層的 Xquery |Microsoft Docs
description: View Xquery 的範例，其中包含階層。
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
ms.openlocfilehash: 21348f838ab51f2352ea975b81688ac0777fe277
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730725"
---
# <a name="xqueries-involving-hierarchy"></a>與階層有關的 XQuery
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

  **AdventureWorks**資料庫中大部分的**xml**類型資料行都是半結構化檔。 因此，儲存在每一個資料列中的文件看起來都不同。 此主題的查詢範例說明如何從這些不同的文件中擷取資訊。  
  
## <a name="examples"></a>範例  
  
### <a name="a-from-the-manufacturing-instructions-documents-retrieve-work-center-locations-together-with-the-first-manufacturing-step-at-those-locations"></a>A. 從製造指示文件中，擷取工作中心位置以及這些位置上的第一個製造步驟  
 若為產品型號7，查詢會 `ManuInstr` 使用**ProductModelID**和**ProductModelName**屬性，以及一或多個 <> 子項目，來建立包含 <> 元素的 XML `Location` 。  
  
 每個 <`Location`> 元素都有自己的屬性集，以及一個 <`step`> 子項目。 這個 <`step`> 子項目是工作中心位置的第一個製造步驟。  
  
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
  
-   [XQuery](../xquery/modules-and-prologs-xquery-prolog.md)初構中的**namespace**關鍵字定義了命名空間前置詞。 稍後在查詢主體中會使用此前置詞。  
  
-   內容切換 Token {) 和 (} 是用來將 XML 建構的查詢切換至查詢評估。  
  
-   **Sql： column （）** 是用來在所結構化的 XML 中包含關聯式值。  
  
-   在建立 <`Location`> 元素時，$wc/@ * 會抓取所有的工作中心位置屬性。  
  
-   **String （）** 函式會傳回 <> 元素的字串值 `step` 。  
  
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
 下列查詢會藉由搜尋整個階層中的 <> 元素，來抓取特定客戶連絡人的其他電話號碼 `telephoneNumber` 。 因為 <`telephoneNumber`> 元素可以出現在階層中的任何位置，所以查詢會在搜尋中使用下階和自我運算子（//）。  
  
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
  
 若只要取出最上層的電話號碼，特別是 <`telephoneNumber`> <> 的子項目 `AdditionalContactInfo` ，則查詢中的 FOR 運算式會變更為  
  
 `for $ph in /ci:AdditionalContactInfo/act:telephoneNumber`.  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 基本概念](../xquery/xquery-basics.md)   
 [&#40;XQuery&#41;的 XML 結構](../xquery/xml-construction-xquery.md)   
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
