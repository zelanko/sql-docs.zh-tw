---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d442a9c397ad184658f9101343e139697c9b3756
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925630"
---
# <a name="dealing-with-failed-updates"></a>處理失敗的更新
當更新結束並出現錯誤時，解決錯誤的方式取決於錯誤的本質和嚴重性，以及應用程式的邏輯。 不過，如果資料庫與其他使用者共用，通常會發生錯誤，那就是其他人在執行之前修改了欄位。 這種類型的錯誤稱為「衝突」。 ADO 會偵測到這種情況並報告錯誤。  
  
## <a name="remarks"></a>備註  
 如果發生更新錯誤，則會在錯誤處理常式中加以攔截。 以 adFilterConflictingRecords 常數篩選記錄集，以便只顯示衝突的資料列。 在此範例中，錯誤解決策略只會列印作者的名字和姓氏（au_fname 和 au_lname）。  
  
 警示使用者發生更新衝突的程式碼看起來像這樣：  
  
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
