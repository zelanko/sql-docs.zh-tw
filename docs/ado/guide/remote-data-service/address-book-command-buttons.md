---
title: "地址通訊錄命令按鈕 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 531e10f28850e6da6f9863cb5f06e253793b1dee
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="address-book-command-buttons"></a>地址通訊錄命令按鈕
通訊錄應用程式包含下列的命令按鈕：  
  
-   A**尋找**提交至資料庫的查詢 按鈕。  
  
-   A**清除**按鈕即可清除文字方塊，再啟動新的搜尋。  
  
-   **更新設定檔**儲存員工記錄的變更 按鈕。  
  
-   A**取消變更**捨棄變更 按鈕。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="find-button"></a>[尋找] 按鈕  
 按一下**尋找**按鈕啟動 VBScript Find_OnClick Sub 程序，這會建置並傳送 SQL 查詢。 按一下此按鈕會填入資料格。  
  
## <a name="building-the-sql-query"></a>建立 SQL 查詢  
 Find_OnClick Sub 程序的第一個部分是 SQL 查詢，一次一個片語附加全域 SQL SELECT 陳述式的文字字串。 它一開始會將變數設定`myQuery`SQL SELECT 陳述式，從資料來源資料表中要求的所有資料列。 接下來，在 Sub 程序會掃描每四個頁面上輸入方塊。  
  
 因為程式會使用 word`like`中建置的 SQL 陳述式，此查詢是子字串搜尋，而不是完全相符項目。  
  
 比方說，如果**姓氏**方塊包含的項目 」 淑真 」 和**標題** 方塊中所包含之項目的 SQL 陳述式 」 程式管理員 」 (值`myQuery`) 會讀取：  
  
```  
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 如果查詢成功，所有的人員姓氏包含文字"淑真 」 （例如淑真和 Berger） 與包含文字 「 程式管理員 」 （例如，程式管理員、 進階技術） 的標題會顯示在 HTML 資料格。  
  
## <a name="preparing-and-sending-the-query"></a>準備和傳送查詢  
 Find_OnClick Sub 程序的最後一個部分是由兩個陳述式所組成。 第一個陳述式會指派[SQL](../../../ado/reference/rds-api/sql-property.md)屬性[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)等於動態建立 SQL 查詢的物件。 第二個陳述式會導致**.RDSDataControl**物件 (`DC1`) 以查詢資料庫，並在方格中顯示新查詢的結果。  
  
```  
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>更新設定檔 按鈕  
 按一下**更新設定檔**按鈕啟動 VBScript Update_OnClick Sub 程序，它會執行[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的 (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)和[重新整理](../../../ado/reference/rds-api/refresh-method-rds.md)方法。  
  
```  
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 當`DC1.SubmitChanges`執行時，遠端資料服務封裝更新資訊，並將它傳送到伺服器，透過 HTTP。 更新是全;如果失敗更新的一部分，進行的任何變更，並會傳回狀態訊息。 `DC1.Refresh`不需要後**SubmitChanges**與遠端資料服務，但是它確保了全新的資料。  
  
## <a name="cancel-changes-button"></a>取消變更 按鈕  
 按一下**取消變更**啟動 VBScript Cancel_OnClick Sub 程序，它會執行[.RDSDataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件的 (`DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md)方法。  
  
```  
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 當`DC1.CancelUpdate`執行時，就會捨棄使用者對員工記錄的資料格上的最後一個查詢或更新後的任何編輯。 它會還原原始值。  
  
## <a name="see-also"></a>另請參閱  
 [解決活頁簿的瀏覽按鈕](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


