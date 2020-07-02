---
title: max 函數（XQuery） |Microsoft Docs
description: 深入瞭解 XQuery max （）函式，此函式會傳回序列中的一個專案，其值大於所有其他專案。
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
- max function [XQuery]
- fn:max function
ms.assetid: 5ee625c0-044a-4cda-b210-02b64e619d65
author: rothja
ms.author: jroth
ms.openlocfilehash: caf736973d288a89bec287aff3cb1c1993e3b0dc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726778"
---
# <a name="aggregate-functions---max"></a>彙總函式 - max
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  從不可部份完成值的序列傳回， *$arg*，其值大於所有其他專案的一個專案。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 不可部份完成值的序列，要從中傳回最大值。  
  
## <a name="remarks"></a>備註  
 所有傳遞至**max （）** 的不可部份完成數值型別，都必須是相同基底類型的子類型。 接受的基底類型是支援**gt**作業的類型。 這些類型包含三個內建數值基底類型以及日期/時間基底類型，它們是 xs:string、xs:boolean 以及 xdt:untypedAtomic。 xdt:untypedAtomic 類型的值會轉換為 xs:double。 如果有混合的這些類型，或如果傳遞其他類型的其他值，就會引發靜態錯誤。  
  
 **Max （）** 的結果會收到傳入類型的基底類型，例如 Xdt： untypedAtomic 的案例中的 xs： double。 如果輸入是靜態空白，則會隱含空白並引發靜態錯誤。  
  
 **Max （）** 函數會傳回序列中的一個值，該值大於輸入序列中的任何其他值。 對於 xs:string 值，會使用預設 Unicode 字碼指標定序。 如果 xdt： untypedAtomic 值無法轉換為 xs： double，則會在輸入序列中忽略此值 *$arg*。 如果輸入是動態計算的空白序列，則會傳回空白序列。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在資料庫的各種**XML**類型資料行中 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 。  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>A. 使用 max() XQuery 函數來尋找製造過程中佔去大部分工時的工作中心位置  
 [Min function （XQuery）](../xquery/aggregate-functions-min.md)中提供的查詢可以重寫以使用**max （）** 函數。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Max （**）函數會將所有整數對應到 xs： decimal。  
  
-   不支援在 xs： duration 類型的值上有**max （）** 函數。  
  
-   不支援跨越基底類型界限的混合類型。  
  
-   不支援提供定序的語法選項。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
