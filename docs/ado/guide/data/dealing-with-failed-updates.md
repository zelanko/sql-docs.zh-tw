---
description: 處理失敗的更新
title: 處理失敗的更新 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
author: rothja
ms.author: jroth
ms.openlocfilehash: c313e424c44ce289254267e6d6aa651308ae25df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453520"
---
# <a name="dealing-with-failed-updates"></a>處理失敗的更新
當更新最後有錯誤時，您解決錯誤的方式取決於錯誤的本質和嚴重性，以及應用程式的邏輯。 但是，如果資料庫與其他使用者共用，則一般的錯誤是其他人會在您進行之前修改欄位。 這類錯誤稱為「衝突」。 ADO 偵測到這種情況並報告錯誤。  
  
## <a name="remarks"></a>備註  
 如果有更新錯誤，則會在錯誤處理常式中被攔截。 使用 adFilterConflictingRecords 常數篩選記錄集，以便只顯示衝突的資料列。 在此範例中，錯誤解決策略只是將作者的名字和姓氏 (au_fname 和 au_lname) 。  
  
 警示使用者發生更新衝突的程式碼如下所示：  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>另請參閱  
 [批次模式](../../../ado/guide/data/batch-mode.md)
