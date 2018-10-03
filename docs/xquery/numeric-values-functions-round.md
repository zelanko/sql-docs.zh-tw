---
title: round 函數 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:round function
- round function [XQuery]
ms.assetid: 320b572f-bd5b-4055-95a6-dec5718c0041
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: eb480cfe18a7f58dfb86a943a4cbdd34fa801138
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47683656"
---
# <a name="numeric-values-functions---round"></a>數值函式 - round
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回最接近引數且去掉小數部份的數字。 如果這樣的數字不止一個，則傳回最接近正無限數的那一個。 例如：  
  
 如果引數是 2.5 **round （)** 傳回 3。  
  
 如果引數為 2.4999， **round （)** 傳回 2。  
  
 如果引數-2.5， **round （)** 傳回-2。  
  
 引數是空的序列，如果**round （)** 傳回空的序列。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 會套用函數的數字。  
  
## <a name="remarks"></a>備註  
 如果類型 *$arg*是三個字的基底類型，其中**xs: float**， **xs: double**，或**xs: decimal**，傳回的型別是相同 *$arg*型別。 如果類型 *$arg*是型別衍生自其中一個數字的類型，傳回的類型是基底的數值類型。  
  
 如果輸入**fn: floor**， **fn: ceiling**，或**fn: round**函式是**xdt: untypedatomic**，不具類型的資料，它會隱含地轉換為**xs: double**。  
  
 任何其他類型都會產生靜態錯誤。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型資料行中的 AdventureWorks 資料庫。  
  
 您可以使用中的工作範例[ceiling 函數 (XQuery)](../xquery/numeric-values-functions-ceiling.md) for **round （)** XQuery 函式。 您只需要會取代**ceiling （)** 查詢中的函式**round （)** 函式。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Round （)** 函式會將整數值對應至 xs: decimal。  
  
-   **Round （)** xs: double 類型 xs: float 值介於-0.5e0 和-0e0 函式會對應到 0e0 而不是-0e0。  
  
## <a name="see-also"></a>另請參閱  
 [floor 函式&#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [ceiling 函式&#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  
