---
title: 通訊錄命令按鈕 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
author: rothja
ms.author: jroth
ms.openlocfilehash: 04f896b4a799e527e2442ef17e69a33f576950dd
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764739"
---
# <a name="address-book-command-buttons"></a>通訊錄命令按鈕
通訊錄應用程式包含下列命令按鈕：  
  
-   用來將查詢提交至資料庫的 [**尋找**] 按鈕。  
  
-   [**清除**] 按鈕，可在開始新的搜尋之前清除文字方塊。  
  
-   [**更新設定檔**] 按鈕，用來儲存員工記錄的變更。  
  
-   [**取消變更**] 按鈕以捨棄變更。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="find-button"></a>尋找按鈕  
 按一下 [**尋找**] 按鈕會啟動 VBScript Find_OnClick Sub 程式，此程式會建立並傳送 SQL 查詢。 按一下此按鈕會填入資料方格。  
  
## <a name="building-the-sql-query"></a>建立 SQL 查詢  
 Find_OnClick Sub 程式的第一個部分會藉由將文字字串附加至全域 SQL SELECT 語句來建立 SQL 查詢，一次一個片語。 首先，將變數設定 `myQuery` 為 SQL SELECT 語句，以要求資料來源資料表中的所有資料列。 接下來，Sub 程式會掃描頁面上的四個輸入方塊。  
  
 因為程式 `like` 會使用建立 SQL 語句中的單字，所以查詢是子字串搜尋，而不是完全相符的專案。  
  
 例如，如果 [**姓氏**] 方塊中包含 "Berge" 專案，而 [**標題**] 方塊包含「程式經理」專案，則會讀取 SQL 語句（的值 `myQuery` ）：  
  
```sql
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 如果查詢成功，則會在 HTML 資料方格中顯示姓氏中包含 "Berge" （例如 Berge 和 Berger）和標題（如 [程式管理員]、[Advanced 技術]）文字的所有人員。  
  
## <a name="preparing-and-sending-the-query"></a>準備和傳送查詢  
 Find_OnClick Sub 程式的最後一個部分是由兩個語句所組成。 第一個語句會指派 RDS 的[SQL](../../../ado/reference/rds-api/sql-property.md)屬性[。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件等於動態建立的 SQL 查詢。 第二個語句會導致**RDS。DataControl** object （ `DC1` ）來查詢資料庫，然後在方格中顯示查詢的新結果。  
  
```vb
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>更新設定檔按鈕  
 按一下 [**更新設定檔**] 按鈕會啟動 VBScript Update_OnClick Sub 程式，這會執行[RDS。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的（ `DC1` ） [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)和[Refresh](../../../ado/reference/rds-api/refresh-method-rds.md)方法。  
  
```vb
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 當 `DC1.SubmitChanges` 執行時，遠端資料服務會封裝所有更新資訊，並透過 HTTP 將它傳送至伺服器。 更新為全部-或-無;如果更新的部分不成功，則不會進行任何變更，而且會傳回狀態訊息。 `DC1.Refresh`在使用遠端資料服務進行**SubmitChanges**後並不需要，但它會確保新的資料。  
  
## <a name="cancel-changes-button"></a>取消變更按鈕  
 按一下 [**取消變更**] 會啟動 VBScript Cancel_OnClick Sub 程式，這會執行[RDS。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的（ `DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md)方法。  
  
```vb
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 當 `DC1.CancelUpdate` 執行時，它會捨棄使用者在上次查詢或更新之後，在資料方格上對員工記錄所做的任何編輯。 它會還原原始值。  
  
## <a name="see-also"></a>另請參閱  
 [通訊錄導覽按鈕](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


