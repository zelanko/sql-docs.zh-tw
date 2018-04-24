---
title: 使用書籤 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c2d4036cbe8205a4dd25c5a1f97ec490b20afa20
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="using-bookmarks"></a>使用書籤
通常會很有用後需要移動直接到特定的記錄傳回**資料錄集**而不需要捲動每一筆記錄，並比較值。 例如，如果您嘗試使用記錄搜尋**尋找**方法，但搜尋會傳回任何記錄，您會自動放置的任一端**資料錄集**。 如果您的提供者支援，可以使用書籤來標示程式的位置之前使用**尋找**方法，使您可以回到您的位置。 書籤是**Variant**輸入可唯一識別中的記錄值**資料錄集**物件。  
  
 您也可以使用書籤的 variant 陣列**資料錄集篩選**方法上將選取的記錄篩選。 如需有關此技術的詳細資訊，請參閱篩選 > 主題中的結果[使用資料錄集](../../../ado/guide/data/working-with-recordsets.md)稍後這一節。  
  
 您可以使用**書籤**屬性來取得書籤記錄，或設定目前的記錄**資料錄集**有效書籤所識別的記錄中的物件。 下列程式碼會使用**書籤**設定書籤，然後傳回已標記書籤記錄之後繼續移至其他記錄的屬性。 若要判斷您**資料錄集**支援書籤，使用**支援**方法。  
  
```  
'BeginBookmarkEg  
Dim varBookmark As Variant  
Dim blnCanBkmrk As Boolean  
  
objRs.Open strSQL, strConnStr, adOpenStatic, adLockOptimistic, adCmdText  
  
If objRs.RecordCount > 4 Then  
    objRs.Move 4                       ' move to the fifth record  
    blnCanBkmrk = objRs.Supports(adBookmark)  
    If blnCanBkmrk = True Then  
        varBookmark = objRs.Bookmark   ' record the bookmark  
        objRs.MoveLast                 ' move to a different record  
        objRs.Bookmark = varBookmark   ' return to the bookmarked (sixth) record  
    End If  
End If  
'EndBookmarkEg  
```  
  
 [支援](../../../ado/reference/ado-api/supports-method.md)稍後涵蓋詳細方法。  
  
 除了 大小寫的複製**資料錄集**，書籤特有**資料錄集**中建立這些，即使使用相同的命令。 這表示您無法使用**書籤**取自一個**資料錄集**移至相同的記錄，第二個**資料錄集**開啟與相同的命令。
