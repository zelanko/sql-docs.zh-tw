---
description: 使用書籤
title: 使用書簽 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
author: rothja
ms.author: jroth
ms.openlocfilehash: 34fc17275609dbf08ffa02a1bc89902c904cac85
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979033"
---
# <a name="using-bookmarks"></a>使用書籤
當您在 **記錄集** 內四處移動之後，直接傳回特定的記錄，而不需要在每一筆記錄中滾動並比較值，通常會很有用。 例如，如果您嘗試使用 **Find** 方法來搜尋記錄，但是搜尋未傳回任何記錄，您就會自動放在 **記錄集**的任一端。 如果您的提供者支援，書簽可以用來在使用 **Find** 方法之前標示您的位置，讓您可以回到您的位置。 書簽是一種 **Variant** 型別值，可唯一識別記錄 **集** 物件中的記錄。  
  
 您也可以使用包含 **記錄集篩選** 方法的書簽變數陣列，以篩選一組選取的記錄。 如需這項技術的詳細資訊，請參閱本節稍後的「使用 [記錄集](../../../ado/guide/data/working-with-recordsets.md)」主題中的篩選結果。  
  
 您可以使用 [ **書簽** ] 屬性來取得記錄的書簽，或是將 **記錄集** 物件中的目前記錄設定為有效書簽所識別的記錄。 下列程式碼會使用 **bookmark** 屬性來設定書簽，然後在移至其他記錄之後返回書簽的記錄。 若要判斷您的 **記錄集** 是否支援書簽，請使用 **支援** 的方法。  
  
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
  
 稍後會更詳細討論 [支援](../../../ado/reference/ado-api/supports-method.md) 方法。  
  
 除了複製的 **記錄集**的情況之外，書簽對它們建立所在的 **記錄集** 是唯一的，即使使用相同的命令也是一樣。 這表示您無法使用從一個**記錄集**取得的**書簽**，移至使用相同命令開啟的第二個**記錄集**內的相同記錄。
