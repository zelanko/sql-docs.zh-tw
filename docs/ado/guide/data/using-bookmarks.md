---
title: 使用書簽 |Microsoft Docs
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
ms.openlocfilehash: 9fa2a738a3e94cd306619a318b75a2fd506972c8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923615"
---
# <a name="using-bookmarks"></a>使用書籤
在**記錄集**內移動之後直接返回特定記錄，而不需要逐一查看每一筆記錄和比較值，通常會很有用。 例如，如果您嘗試使用**Find**方法搜尋記錄，但搜尋未傳回任何記錄，則會自動放在**記錄集**的任一端。 如果您的提供者支援這些專案，您可以使用書簽來標示您的位置，然後再使用**Find**方法，讓您可以回到您的位置。 書簽是一種**Variant**類型值，可唯一識別記錄**集**物件中的記錄。  
  
 您也可以使用書簽的 variant 陣列搭配**記錄集篩選**方法，來篩選選取的一組記錄。 如需這項技術的詳細資訊，請參閱本節稍後的使用[記錄集](../../../ado/guide/data/working-with-recordsets.md)主題中的篩選結果。  
  
 您可以使用 [**書簽**] 屬性來取得記錄的書簽，或將**記錄集**物件中的目前記錄設定為有效書簽所識別的記錄。 下列程式碼會使用 [**書簽**] 屬性來設定書簽，然後在移至其他記錄之後回到已加入書簽的記錄。 若要判斷您的**記錄集**是否支援書簽，請使用**支援**方法。  
  
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
  
 稍後會詳細討論[支援](../../../ado/reference/ado-api/supports-method.md)方法。  
  
 除了複製的**記錄集**的案例之外，書簽對於建立它們的**記錄集**而言是唯一的，即使使用相同的命令也一樣。 這表示您無法使用從一個**記錄集**取得的**書簽**，移至以相同命令開啟之第二個**記錄集**的相同記錄。
