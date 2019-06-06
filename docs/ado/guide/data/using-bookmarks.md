---
title: 使用書籤 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c7e14e063d1aabcfce6391a85c0fcddbf0ff4e9f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704613"
---
# <a name="using-bookmarks"></a>使用書籤
通常很有用直接傳回到特定記錄後需要四處移動**資料錄集**而不需捲動以查看每一筆記錄，並比較值。 比方說，如果您嘗試使用記錄搜尋**尋找**方法，但搜尋未傳回資料錄，您會自動放置在兩端**資料錄集**。 如果您的提供者支援它們，書籤可用來將您的位置標記之前使用**尋找**方法，讓您可以返回您的位置。 書籤**Variant**輸入可唯一識別中的記錄值**資料錄集**物件。  
  
 您也可以使用 variant 的陣列，與書籤**資料錄集篩選器**方法來篩選一組選取的記錄。 如需這項技術的詳細資訊，請參閱篩選 > 主題中的結果[使用資料錄集](../../../ado/guide/data/working-with-recordsets.md)稍後這一節。  
  
 您可以使用**書籤**屬性來取得書籤的記錄，或在中設定目前資料錄**資料錄集**物件的有效書籤所識別的記錄。 下列程式碼會使用**書籤**来設定書籤，然後再返回加上書籤的資料錄之後繼續移至其他記錄, 屬性。 若要判斷您**Recordset**支援書籤，使用**支援**方法。  
  
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
  
 [支援](../../../ado/reference/ado-api/supports-method.md)方法稍後會討論更多詳細資料中。  
  
 除了的情況下複製**資料錄集**，書籤特有**資料錄集**中建立這些，即使使用相同的命令。 這表示您無法使用**書籤**取自一個**資料錄集**若要移到相同的記錄，每秒**資料錄集**開啟使用相同的命令。
