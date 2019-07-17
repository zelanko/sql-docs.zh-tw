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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d1aa5b628bec9399374b94a2cd78090207bf09b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922989"
---
# <a name="address-book-command-buttons"></a>通訊錄命令按鈕
通訊錄應用程式包含下列的命令按鈕：  
  
-   A**尋找**按鈕來提交查詢到資料庫。  
  
-   A**清除**按鈕以開始新的搜尋之前清除文字方塊。  
  
-   **更新設定檔**將變更儲存到員工記錄的按鈕。  
  
-   A**取消變更**來捨棄變更 按鈕。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="find-button"></a>[尋找] 按鈕  
 按一下 **尋找**按鈕會啟用 VBScript Find_OnClick Sub 程序，建置並傳送的 SQL 查詢。 按一下此按鈕會填入資料格。  
  
## <a name="building-the-sql-query"></a>建立 SQL 查詢  
 Find_OnClick 子函數程序的第一個部分將文字字串附加至通用的 SQL SELECT 陳述式，以建置 SQL 查詢，一次一個片語。 它一開始會設定變數`myQuery`要求所有資料列從資料來源資料表的 SQL SELECT 陳述式。 接下來，在 Sub 程序會掃描每個頁面上的四個輸入方塊。  
  
 因為程式會使用這個字`like`建置 SQL 陳述式，此查詢也是子字串搜尋，而不是完全相符項目。  
  
 比方說，如果**姓氏** 方塊中所包含的項目"宜芳 」 並**標題** 方塊中所包含的項目 「 經理 」，SQL 陳述式 (值`myQuery`) 會讀取：  
  
```sql
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 如果查詢成功，含有文字"宜芳 」 （例如宜芳和 Berger） 的最後一個名稱和標題，其中包含文字 「 程式管理員 」 （例如，專案經理、 進階的技術） 的所有人員會都顯示 HTML 資料方格中。  
  
## <a name="preparing-and-sending-the-query"></a>準備並傳送查詢  
 Find_OnClick 子函數程序的最後一個部分是由兩個陳述式所組成。 第一個陳述式指派[SQL](../../../ado/reference/rds-api/sql-property.md)屬性[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)等於動態建立的 SQL 查詢的物件。 第二個陳述式會導致**rds。DataControl**物件 (`DC1`) 以查詢資料庫，並在方格中顯示新查詢的結果。  
  
```vb
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>更新設定檔 按鈕  
 按一下 [**更新設定檔**] 按鈕會啟用 VBScript Update_OnClick Sub 程序，它會執行[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的 (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)並[重新整理](../../../ado/reference/rds-api/refresh-method-rds.md)方法。  
  
```vb
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 當`DC1.SubmitChanges`執行時，遠端資料服務封裝更新的所有資訊，並將它傳送到透過 HTTP 伺服器。 更新是孤注一擲;如果在更新期間失敗時，所做的變更都不是，並會傳回狀態訊息。 `DC1.Refresh` 不需要在後**SubmitChanges**與遠端資料服務，但它可確保新的資料。  
  
## <a name="cancel-changes-button"></a>取消變更按鈕  
 按一下 **取消變更**會啟用 VBScript Cancel_OnClick Sub 程序，它會執行[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的 (`DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md)方法。  
  
```vb
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 當`DC1.CancelUpdate`執行時，它會捨棄使用者已自最後一個查詢或更新時對員工記錄的資料格上的任何編輯。 它會還原原始值。  
  
## <a name="see-also"></a>另請參閱  
 [通訊錄導覽按鈕](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


