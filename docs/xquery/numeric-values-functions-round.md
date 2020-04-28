---
title: round 函數（XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:round function
- round function [XQuery]
ms.assetid: 320b572f-bd5b-4055-95a6-dec5718c0041
author: rothja
ms.author: jroth
ms.openlocfilehash: 1927d6e483683699196cfc7e87928f27bf23446a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67946549"
---
# <a name="numeric-values-functions---round"></a>數值函式 - round
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回最接近引數且去掉小數部份的數字。 如果這樣的數字不止一個，則傳回最接近正無限數的那一個。 例如：  
  
 如果引數為2.5， **round （）** 會傳回3。  
  
 如果引數為2.4999， **round （）** 會傳回2。  
  
 如果引數為-2.5， **round （）** 會傳回-2。  
  
 如果引數是空的序列， **round （）** 就會傳回空的序列。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 會套用函數的數字。  
  
## <a name="remarks"></a>備註  
 如果 *$arg*的類型是三個數值基底類型之一（ **xs： float**、 **xs： double**或**xs： decimal**），則傳回類型與 *$arg*類型相同。 如果 *$arg*的類型是衍生自其中一個數數值型別的類型，則傳回類型會是基底數數值型別。  
  
 如果**fn： floor**、 **fn：天花板**或**fn： round**函數的輸入是**xdt： untypedAtomic**、不具類型的資料，它會隱含地轉換為**xs： double**。  
  
 任何其他類型都會產生靜態錯誤。  
  
## <a name="examples"></a>範例  
 本主題針對儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中的 xml 實例提供 XQuery 範例。  
  
 您可以針對**round （）** XQuery 函數使用[上限函數（XQuery）](../xquery/numeric-values-functions-ceiling.md)中的工作範例。 您只需要將查詢中的**上限（）** 函數取代為**round （）** 函式即可。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Round （）** 函數會將整數值對應至 xs： decimal。  
  
-   Xs： double 和 xs： float 值介於-0.5 e0 和-0e0 之間的**round （）** 函數會對應到0e0，而不是-0e0。  
  
## <a name="see-also"></a>另請參閱  
 [floor 函數 &#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [&#40;XQuery&#41;的上限函數](../xquery/numeric-values-functions-ceiling.md)  
  
  
