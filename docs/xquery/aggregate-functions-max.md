---
title: max 函數 (XQuery) |Microsoft 文件
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
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
- max function [XQuery]
- fn:max function
ms.assetid: 5ee625c0-044a-4cda-b210-02b64e619d65
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b0b8672ab3a93b8dc71e8f3d44175fa209c7583f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="aggregate-functions---max"></a>最大值彙總函式-
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  從不可部份完成值的序列傳回 *$arg*，其值大於所有其他的項目。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 不可部份完成值的序列，要從中傳回最大值。  
  
## <a name="remarks"></a>備註  
 所有類型的不可部份完成值傳遞至**max （)** 必須是相同的基底類型的子類型。 接受的基底類型的類型，可支援**gt**作業。 這些類型包含三個內建數值基底類型以及日期/時間基底類型，它們是 xs:string、xs:boolean 以及 xdt:untypedAtomic。 xdt:untypedAtomic 類型的值會轉換為 xs:double。 如果沒有混用這些類型，或其他類型的其他值會傳遞，就會引發靜態錯誤。  
  
 結果**max （)** 接收傳入的類型，例如 xdt 的 xs: double 類型的基底類型。 如果輸入是靜態空白，則會隱含空白並引發靜態錯誤。  
  
 **Max （)** 函式會傳回一個值大於輸入序列中的任何其他的順序。 對於 xs:string 值，會使用預設 Unicode 字碼指標定序。 如果 xdt: untypedatomic 值無法轉換成 xs: double，值會忽略輸入序列中 *$arg*。 如果輸入是動態計算的空白序列，則會傳回空白序列。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型資料行中的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]資料庫。  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>A. 使用 max() XQuery 函數來尋找製造過程中佔去大部分工時的工作中心位置  
 中提供的查詢[min 函數 (XQuery)](../xquery/aggregate-functions-min.md)可以改寫為使用**max （)** 函式。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Max (**) 函式會將所有整數都對應至 xs: decimal。  
  
-   **Max （)** 不支援的 xs: duration 類型值的函數。  
  
-   不支援跨越基底類型界限的混合類型。  
  
-   不支援提供定序的語法選項。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
