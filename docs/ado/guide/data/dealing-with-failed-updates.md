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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925630"
---
# <a name="dealing-with-failed-updates"></a>處理失敗的更新
當更新已結束但發生錯誤時，解決錯誤的方式而定的本質和 錯誤嚴重性以及您的應用程式的邏輯。 不過，如果資料庫與其他使用者共用，常見的錯誤將會有其他人修改的欄位，然後才執行。 此類錯誤稱為 「 衝突 」。 ADO 會偵測這種情況，並回報錯誤。  
  
## <a name="remarks"></a>備註  
 如果有更新錯誤，它們會受困在錯誤處理常式。 這樣的衝突資料列就可以看到，篩選與 adFilterConflictingRecords 常數資料錄集。 在此範例中，錯誤解決方案策略是只列印作者的名字和姓氏的名稱 （au_fname 和 au_lname）。  
  
 若要通知使用者有更新衝突的程式碼看起來像這樣：  
  
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
