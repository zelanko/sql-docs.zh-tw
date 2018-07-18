---
title: 處理失敗的更新 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- updates [ADO], dealing with failed updates
ms.assetid: 299c37bd-19ff-4261-8571-b9665687e075
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45e5a20e0527f8b30035aef7ff86a90378039b69
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270187"
---
# <a name="dealing-with-failed-updates"></a>處理失敗的更新
更新已結束但發生錯誤，當您解決錯誤的方式取決於本質和錯誤的嚴重性和應用程式的邏輯。 不過，如果資料庫與其他使用者共用，常見的錯誤將會有其他人修改欄位，然後再進行。 這種類型的錯誤稱為衝突。 ADO 會偵測這種情況，並報告錯誤。  
  
## <a name="remarks"></a>備註  
 如果沒有更新錯誤，它們將會陷在錯誤處理常式中。 篩選與 adFilterConflictingRecords 常數資料錄集，使衝突資料列會顯示。 在此範例中，錯誤解決方案策略是只列印作者的名字和姓氏的名稱 （au_fname 和 au_lname）。  
  
 警示使用者更新衝突的程式碼看起來像這樣：  
  
```  
objRs.Filter = adFilterConflictingRecords  
objRs.MoveFirst  
Do While Not objRst.EOF  
   Debug.Print "Conflict: Name =  "; objRs!au_fname; " "; objRs!au_lname  
   objRs.MoveNext  
Loop  
```  
  
## <a name="see-also"></a>另請參閱  
 [批次模式](../../../ado/guide/data/batch-mode.md)
