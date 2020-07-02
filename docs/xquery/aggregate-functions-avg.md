---
title: avg 函數（XQuery） |Microsoft Docs
description: 深入瞭解 XQuery 函數 avg （），此函式會傳回指定之數位序列的平均值。
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
- fn:avg function
- avg function [XQuery]
ms.assetid: 0cc60267-3c56-4a88-8ad7-bb07f0255d56
author: rothja
ms.author: jroth
ms.openlocfilehash: a5ee393faed7f88bb155527d2233285d142b3a09
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726787"
---
# <a name="aggregate-functions---avg"></a>彙總函式 - avg
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

  傳回數字序列的平均值。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:avg($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 不可部份完成值的序列，會計算其平均值。  
  
## <a name="remarks"></a>備註  
 傳遞至**avg （）** 的不可部份完成值之所有類型，都必須是其中一個內建數值基底類型或 Xdt： untypedAtomic 的子類型。 它們不能是混合的類型。 xdt:untypedAtomic 類型的值會被視為 xs:double。 **Avg （）** 的結果會收到傳入類型的基底類型，例如 Xdt： untypedAtomic 的情況下的 xs： double。  
  
 如果輸入是靜態空白，則會隱含空白並引發靜態錯誤。  
  
 **Avg （）** 函數會傳回計算所得數位的平均值。 例如：  
  
 **sum （** *$arg* **） div count （** *$arg* **）**  
  
 如果 *$arg*是空的序列，則會傳回空的序列。  
  
 如果 xdt： untypedAtomic 值無法轉換為 xs： double，則會在輸入序列中忽略此值 *$arg*。  
  
 在其他所有的情況中，此函數會傳回靜態錯誤。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中。  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>A. 使用 avg() XQuery 函數，尋找在製造過程中，工時大於所有工作中心位置平均工時的工作中心位置。  
 您可以重寫[min function （XQuery）](../xquery/aggregate-functions-min.md)中提供的查詢，以使用**avg （）** 函數。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Avg （）** 函數會將所有整數對應到 xs： decimal。  
  
-   不支援 xs： duration 類型值的**avg （）** 函數。  
  
-   不支援跨越基底類型界限的混合類型。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
