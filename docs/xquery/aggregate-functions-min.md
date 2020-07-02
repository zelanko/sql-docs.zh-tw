---
title: min 函數（XQuery） |Microsoft Docs
description: 深入瞭解 XQuery min （）函式，此函式會傳回序列中的一個專案，而該值的值比其他所有其他專案少。
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
- fn:min function
- min function [XQuery]
ms.assetid: db0b7d94-3fa6-488f-96d6-6a9a7d6eda23
author: rothja
ms.author: jroth
ms.openlocfilehash: 1f2fc71e138fc2377d8f09c50250bbfe39077686
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718157"
---
# <a name="aggregate-functions---min"></a>彙總函式 - min
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  從不可部份完成值的序列傳回， *$arg*，其值小於所有其他專案的一個專案。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:min($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 從項目序列傳回最小值。  
  
## <a name="remarks"></a>備註  
 所有傳遞至**min （）** 的不可部份完成數值型別，都必須是相同基底類型的子類型。 接受的基底類型是支援**gt**作業的類型。 這些類型包含三個內建數值基底類型以及日期/時間基底類型，它們是 xs:string、xs:boolean 以及 xdt:untypedAtomic。 xdt:untypedAtomic 類型的值會轉換為 xs:double。 如果有混合的這些類型，或如果傳遞其他類型的其他值，就會引發靜態錯誤。  
  
 **Min （）** 的結果會收到傳入類型的基底類型，例如 Xdt： untypedAtomic 的案例中的 xs： double。 如果輸入是靜態空白，則會隱含空白並傳回靜態錯誤。  
  
 **Min （）** 函數會傳回序列中的一個值，該值小於輸入序列中的任何其他值。 對於 xs:string 值，會使用預設 Unicode 字碼指標定序。 如果 xdt： untypedAtomic 值無法轉換為 xs： double，則會在輸入序列中忽略此值 *$arg*。 如果輸入是動態計算的空白序列，則會傳回空白序列。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中。  
  
### <a name="a-using-the-min-xquery-function-to-find-the-work-center-location-that-has-the-fewest-labor-hours"></a>A. 使用 min() XQuery 函數尋找包含最少工時的工作中心位置  
 下列查詢擷取在製造產品型號 (ProductModelID=7) 的過程中，包含最少工時的所有工作中心位置。 一般而言，會傳回單一位置，如下所示。 如果有多個位置包含相等的最少工時數目，就會將它們全部傳回。  
  
```  
select ProductModelID, Name, Instructions.query('  
  declare namespace AWMI=  
    "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  for   $Location in /AWMI:root/AWMI:Location  
  where $Location/@LaborHours =  
          min( /AWMI:root/AWMI:Location/@LaborHours )  
return  
  <Location WCID=     "{ $Location/@LocationID }"   
              LaborHrs= "{ $Location/@LaborHours }" />  
  ') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   XQuery 初構中的**namespace**關鍵字定義了命名空間前置詞。 之後會在 XQuery 主體中使用前置詞。  
  
 XQuery 主體會 \<Location> 以具有 WCID 和**LaborHrs**屬性的元素來建立 XML。  
  
-   該查詢也會擷取 ProductModelID 與名稱值。  
  
 以下是結果：  
  
```  
ProductModelID   Name              Result  
---------------  ----------------  ---------------------------------  
7                HL Touring Frame  <Location WCID="45" LaborHrs="0.5"/>   
```  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Min （）** 函數會將所有整數對應到 xs： decimal。  
  
-   不支援 xs： duration 類型值的**min （）** 函數。  
  
-   不支援跨越基底類型界限的混合類型。  
  
-   不支援提供定序的語法選項。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
