---
title: floor 函數 (XQuery) |Microsoft Docs
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
- floor function [XQuery]
- fn:floor function
ms.assetid: 4ace57dd-b66e-4b60-a2b9-a1b0f1a0831d
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c27e432dc258b4d2b9d21bfe0ab28df8ee5b510
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946538"
---
# <a name="numeric-values-functions---floor"></a>數值函式 - floor
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回不含小數、不大於其引數值的最大數字。 如果引數是空的序列，它會傳回空的序列。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 會套用函數的數字。  
  
## <a name="remarks"></a>備註  
 如果類型 *$arg*是三個字的基底類型，其中**xs: float**， **xs: double**，或**xs: decimal**，傳回的型別是相同 *$arg*型別。 如果類型 *$arg*是型別衍生自其中一個數字的類型，傳回的類型是基底的數值類型。  
  
 Fn: floor、 fn: ceiling 或 fn: round 函數的輸入是否**xdt: untypedatomic**，不具類型的資料，它會隱含地轉換為**xs: double**。 任何其他類型都會產生靜態錯誤。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存於各種**xml**類型資料行中的 AdventureWorks 範例資料庫。  
  
 您可以使用中的工作範例[ceiling 函數 (XQuery)](../xquery/numeric-values-functions-ceiling.md) for **floor （)** XQuery 函式。 您只需要會取代**ceiling （)** 查詢中的函式**floor （)** 函式。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Floor （)** 函式會將所有的整數值對應至 xs: decimal。  
  
## <a name="see-also"></a>另請參閱  
 [ceiling 函式&#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)   
 [round 函式&#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)   
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
