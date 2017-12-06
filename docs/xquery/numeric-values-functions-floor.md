---
title: "floor 函數 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- floor function [XQuery]
- fn:floor function
ms.assetid: 4ace57dd-b66e-4b60-a2b9-a1b0f1a0831d
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 41dee329166c3c791a5caf0d5a31393278a96d5d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="numeric-values-functions---floor"></a>Floor 數值值函式-
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
 如果類型*$arg*是三個字的基底類型，其中**xs: float**， **xs: double**，或**xs: decimal**，是相同的傳回型別*$arg*型別。 如果類型*$arg*是衍生自其中一個數字類型，類型的傳回型別是基底的數值類型。  
  
 如果 fn: floor、 fn: ceiling 或 fn: round 函數的輸入是**xdt: untypedatomic**，不具類型的資料，它會隱含地轉換為**xs: double**。 任何其他類型都會產生靜態錯誤。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型資料行中的 AdventureWorks 範例資料庫。  
  
 您可以使用中的工作範例[ceiling 函數 (XQuery)](../xquery/numeric-values-functions-ceiling.md)如**floor** XQuery 函式。 您只需要為取代**ceiling （)**函式中使用查詢**floor**函式。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Floor**函式會將所有的整數值對應至 xs: decimal。  
  
## <a name="see-also"></a>請參閱  
 [ceiling 函數 &#40;XQuery &#41;](../xquery/numeric-values-functions-ceiling.md)   
 [round 函式 &#40;XQuery &#41;](../xquery/numeric-values-functions-round.md)   
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
