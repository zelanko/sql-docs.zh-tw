---
description: 通訊錄命令按鈕
title: 通訊錄命令按鈕 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: d234732b90fdd89b6f0e41efe1762bb3a99ddde2
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724849"
---
# <a name="address-book-command-buttons"></a>通訊錄命令按鈕
通訊錄的應用程式包含下列命令按鈕：  
  
-   將查詢提交至資料庫的 [ **尋找** ] 按鈕。  
  
-   在開始新的搜尋之前清除文字方塊的 **清除** 按鈕。  
  
-   用來儲存員工記錄變更的 [ **更新設定檔** ] 按鈕。  
  
-   [ **取消變更** ] 按鈕以捨棄變更。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="find-button"></a>尋找按鈕  
 按一下 [ **尋找** ] 按鈕會啟動 VBScript Find_OnClick Sub 程式，此程式會建立並傳送 SQL 查詢。 按一下這個按鈕，就會填入資料格。  
  
## <a name="building-the-sql-query"></a>建立 SQL 查詢  
 Find_OnClick Sub 程式的第一個部分會將文字字串附加至全域 SQL SELECT 語句，以一次一個句子的方式建立 SQL 查詢。 首先，將變數設定 `myQuery` 為 SQL SELECT 語句，以要求資料來源資料表中的所有資料列。 接下來，副程式會掃描頁面上的四個輸入方塊。  
  
 由於程式 `like` 會使用建立 SQL 語句中的字組，因此查詢會是子字串搜尋，而不是完全相符的專案。  
  
 例如，如果 [ **姓氏** ] 方塊包含專案 "Berge"，而 **標題** 方塊中包含 "Program Manager" 專案，則) 的 SQL 語句 (值 `myQuery` 會讀取：  
  
```sql
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 如果查詢成功，則具有姓氏的所有人員（包含 "Berge" 文字） (例如 Berge 和 Berger) ，而且標題中包含 "Program Manager" 單字 (例如，[程式管理員]、[先進技術) ] 會顯示在 HTML 資料方格中。  
  
## <a name="preparing-and-sending-the-query"></a>準備和傳送查詢  
 Find_OnClick Sub 程式的最後一個部分是由兩個語句所組成。 第一個語句會指派 RDS 的 [SQL](../../reference/rds-api/sql-property.md) 屬性 [。DataControl](../../reference/rds-api/datacontrol-object-rds.md) 物件等於動態建立的 SQL 查詢。 第二個語句會導致 **RDS。DataControl** 物件 (`DC1`) 來查詢資料庫，然後在方格中顯示查詢的新結果。  
  
```vb
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>更新設定檔按鈕  
 按一下 [ **更新設定檔** ] 按鈕會啟動 VBScript Update_OnClick Sub 程式，它會執行 [RDS。DataControl](../../reference/rds-api/datacontrol-object-rds.md) 物件的 (`DC1`) [SubmitChanges](../../reference/rds-api/submitchanges-method-rds.md) 和 [Refresh](../../reference/rds-api/refresh-method-rds.md) 方法。  
  
```vb
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 當 `DC1.SubmitChanges` 執行時，遠端資料服務會封裝所有更新資訊，並透過 HTTP 將其傳送至伺服器。 更新為全部或不是任何專案;如果更新的一部分不成功，則不會進行任何變更，而且會傳回狀態訊息。 `DC1.Refresh` 在使用遠端資料服務進行 **SubmitChanges** 之後不需要，但可確保新的資料。  
  
## <a name="cancel-changes-button"></a>取消變更按鈕  
 按一下 [ **取消變更** ] 會啟動 VBScript Cancel_OnClick Sub 程式，這會執行 [RDS。DataControl](../../reference/rds-api/datacontrol-object-rds.md) 物件的 (`DC1)` [CancelUpdate](../../reference/rds-api/cancelupdate-method-rds.md) 方法。  
  
```vb
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 當 `DC1.CancelUpdate` 執行時，它會在上次查詢或更新之後，捨棄使用者對資料方格上的員工記錄所做的任何編輯。 它會還原原始的值。  
  
## <a name="see-also"></a>另請參閱  
 [通訊錄導覽按鈕](./address-book-navigation-buttons.md)   
 [DataControl 物件 (RDS)](../../reference/rds-api/datacontrol-object-rds.md)