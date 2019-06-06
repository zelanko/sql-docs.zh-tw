---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 370ea53d652f88f1870d81440e6a676cbc29da26
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718337"
---
# <a name="address-book-navigation-buttons"></a>通訊錄導覽按鈕
通訊錄應用程式會顯示在網頁底部的瀏覽按鈕。 第一個或最後一個資料列的資料或目前的選取範圍的相鄰的資料列，您可以使用瀏覽按鈕來選取導覽中的 HTML 方格中顯示的資料。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="navigation-sub-procedures"></a>瀏覽 Sub 程序  
 通訊錄應用程式包含數個程序，可讓使用者按一下 [**第一**，**下一步]** ，**上一步**，以及**最後一個**若要將資料移動的按鈕。  
  
 例如，按一下**第一個**按鈕會啟用 VBScript First_OnClick Sub 程序。 執行程序[MoveFirst](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)方法，讓目前的選取範圍的第一個資料列。 按一下 [**上次**] 按鈕啟動 Last_OnClick Sub 程序，這會叫用[MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)方法，讓資料的最後一個資料列目前的選取範圍。 其餘的瀏覽按鈕運作方式類似。  
  
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
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)



