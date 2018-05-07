---
title: avg 函數 (XQuery) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:avg function
- avg function [XQuery]
ms.assetid: 0cc60267-3c56-4a88-8ad7-bb07f0255d56
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6c347eb78dd3ac8e58075cc91edeee87b3a4418d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="aggregate-functions---avg"></a>彙總函式-avg
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回數字序列的平均值。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:avg($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 不可部份完成值的序列，會計算其平均值。  
  
## <a name="remarks"></a>備註  
 所有類型的不可部份完成值傳遞至**avg （)** 必須只有其中三種內建數值基底類型或 xdt: untypedatomic 的子類型。 它們不能是混合的類型。 xdt:untypedAtomic 類型的值會被視為 xs:double。 結果**avg （)** 接收傳入的類型，例如 xdt 的 xs: double 類型的基底類型。  
  
 若輸入在靜態上是空的，則隱含著空值且會引發靜態錯誤。  
  
 **Avg （)** 函式會傳回計算數字的平均值。 例如：  
  
 **sum (** *$arg* **) div 計數 (** *$arg* **)**  
  
 如果 *$arg*是空的序列，傳回空的序列。  
  
 如果 xdt: untypedatomic 值無法轉換成 xs: double，值會忽略輸入序列中 *$arg*。  
  
 在其他所有的情況中，此函數會傳回靜態錯誤。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型 AdventureWorks 資料庫中的資料行。  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>A. 使用 avg() XQuery 函數，尋找在製造過程中，工時大於所有工作中心位置平均工時的工作中心位置。  
 您可以重寫查詢中提供[min 函數 (XQuery)](../xquery/aggregate-functions-min.md)使用**avg （)** 函式。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Avg （)** 函式會將所有整數都對應至 xs: decimal。  
  
-   **Avg （)** 不支援的 xs: duration 類型值的函數。  
  
-   不支援跨越基底類型界限的混合類型。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
