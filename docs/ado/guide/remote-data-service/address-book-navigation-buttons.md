---
description: 通訊錄導覽按鈕
title: 通訊錄導覽按鈕 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], navigation buttons
- address book application scenario [ADO], navigation buttons
ms.assetid: f0dd84c6-5c33-4ab9-82b4-4c42dfdd2277
author: rothja
ms.author: jroth
ms.openlocfilehash: 03959b22d0b64f2932326c42f5bb0117441b9051
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88758648"
---
# <a name="address-book-navigation-buttons"></a>通訊錄導覽按鈕
通訊錄應用程式會在網頁底部顯示導覽按鈕。 您可以使用瀏覽按鈕，選取資料的第一個或最後一個資料列，或與目前選取範圍連續的資料列，以流覽 HTML 方格顯示中的資料。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="navigation-sub-procedures"></a>導覽 Sub 程式  
 通訊錄的應用程式包含數個程式，可讓使用者按一下 **第一個**、 **下**一個、 **上**一個和 **最後一個** 按鈕來四處移動資料。  
  
 例如，按一下 **第一個** 按鈕會啟動 VBScript First_OnClick Sub 程式。 此程式會執行 [MoveFirst](../../reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) 方法，這會讓第一個資料列成為目前的選取專案。 按一下 [ **上一步** ] 按鈕會啟動 Last_OnClick Sub 程式，它會叫用 [MoveLast](../../reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) 方法，將最後一個資料列設為目前的選取範圍。 其餘的瀏覽按鈕會以類似的方式運作。  
  
```vb
' Move to the first record in the bound Recordset.  
Sub First_OnClick  
   DC1.Recordset.MoveFirst  
End Sub  
  
' Move to the next record from the current position   
' in the bound Recordset.  
Sub Next_OnClick  
   If Not DC1.Recordset.EOF Then    ' Cannot move beyond bottom record.  
      DC1.Recordset.MoveNext  
      Exit Sub  
   End If     
End Sub  
  
' Move to the previous record from the current position in the bound   
' Recordset.  
Sub Prev_OnClick  
   If Not DC1.Recordset.BOF Then    ' Cannot move beyond top record.  
      DC1.Recordset.MovePrevious  
      Exit Sub  
   End If  
End Sub  
  
' Move to the last record in the bound Recordset.  
Sub Last_OnClick  
   DC1.Recordset.MoveLast  
End Sub  
```  
  
## <a name="see-also"></a>另請參閱  
 [DataControl 物件 (RDS) ](../../reference/rds-api/datacontrol-object-rds.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (RDS)](../../reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)