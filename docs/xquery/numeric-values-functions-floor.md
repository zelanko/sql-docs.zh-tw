---
title: floor 函數（XQuery） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
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
 如果 *$arg*的類型是三個數值基底類型之一（ **xs： float**、 **xs： double**或**xs： decimal**），則傳回類型與 *$arg*類型相同。 如果 *$arg*的類型是衍生自其中一個數數值型別的類型，則傳回類型會是基底數數值型別。  
  
 如果 fn： floor、fn：天花板或 fn： round 函數的輸入是**xdt： untypedAtomic**、不具類型的資料，它會隱含地轉換為**xs： double**。 任何其他類型都會產生靜態錯誤。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 範例資料庫的各種**xml**類型資料行中。  
  
 您可以針對**floor （）** XQuery 函數使用[上限函數（XQuery）](../xquery/numeric-values-functions-ceiling.md)中的工作範例。 您只需要將查詢中的**上限（）** 函數取代為**floor （）** 函式即可。  
  
## <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Floor （）** 函數會將所有整數值對應至 xs： decimal。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;XQuery&#41;的上限函數](../xquery/numeric-values-functions-ceiling.md)   
 [round 函數 &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)   
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
