---
title: count 函數（XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:count function
- count function [XQuery]
ms.assetid: a9f7131f-23e1-4d4d-a36c-180447543926
author: rothja
ms.author: jroth
ms.openlocfilehash: a359251dbb2bd2a2685e5d9fb91d5c1603950c25
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67986309"
---
# <a name="aggregate-functions---count"></a>彙總函式 - count
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回 *$arg*所指定序列中包含的專案數。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:count($arg as item()*) as xs:integer  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 要計數的項目  
  
## <a name="remarks"></a>備註  
 如果 *$arg*是空的序列，則傳回0。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中。  
  
### <a name="a-using-the-count-xquery-function-to-count-the-number-of-work-center-locations-in-the-manufacturing-of-a-product-model"></a>A. 使用 count() XQuery 函數計數在製造產品型號時工作中心的位置數目  
 下列查詢計數在製造產品型號的過程中 (ProductModelID=7) 工作中心的位置數目。  
  
```  
SELECT Production.ProductModel.ProductModelID,   
       Production.ProductModel.Name,   
       Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations>  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID=7  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   [XQuery](../xquery/modules-and-prologs-xquery-prolog.md)初構中的**namespace**關鍵字定義了命名空間前置詞。 之後會在 XQuery 主體中使用前置詞。  
  
-   查詢會建立包含 <`NoOfWorkStations`> 元素的 XML。  
  
-   XQuery 主體中的**count （）** 函式會計算 <`Location`> 元素的數目。  
  
 以下是結果：  
  
```  
ProductModelID   Name                 WorkCtrCount       
-------------- ---------------------------------------------------  
7             HL Touring Frame  <NoOfWorkStations>6</NoOfWorkStations>     
```  
  
 您也可以建構 XML 以包含產品型號識別碼及名稱，如下列查詢所示：  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations  
             ProductModelID= "{ sql:column("Production.ProductModel.ProductModelID") }"   
             ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID= 7  
```  
  
 以下是結果：  
  
```  
<NoOfWorkStations ProductModelID="7"   
                  ProductModelName="HL Touring Frame">6</NoOfWorkStations>  
```  
  
 除了 XML 之外，您可用非 xml 類型來傳回這些值，如下列查詢所示。 查詢會使用[value （）方法（xml 資料類型）](../t-sql/xml/value-method-xml-data-type.md)來取出工作中心位置計數。  
  
```  
SELECT  ProductModelID,   
        Name,   
        Instructions.value('declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
           count(/AWMI:root/AWMI:Location)', 'int' ) as WorkCtrCount  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 以下是結果：  
  
```  
ProductModelID    Name            WorkCtrCount  
-------------- ---------------------------------  
7              HL Touring Frame        6     
```  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
