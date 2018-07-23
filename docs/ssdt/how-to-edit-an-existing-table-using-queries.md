---
title: 如何：使用查詢編輯現有的資料表 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 58f4de8e-97b4-4bcb-953f-f3d428432491
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 541310addcd1b9fec25038e962197a1b06eea34a
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39088530"
---
# <a name="how-to-edit-an-existing-table-using-queries"></a>如何：使用查詢編輯現有的資料表
您可以撰寫 Transact\-SQL 查詢，編輯資料表的定義或資料。 若要以視覺化方式在資料表中檢視或輸入資料，請使用資料編輯器，如[連接的資料庫開發](../ssdt/connected-database-development.md)所述。  
  
> [!WARNING]  
> 下列程序將使用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)小節的程序中所建立的實體。  
  
### <a name="to-edit-the-definition-of-an-existing-table"></a>若要編輯現有資料表的定義  
  
1.  在 [SQL Server 物件總管] 中，展開 [Trade] 資料庫的 [資料表] 節點，然後以滑鼠右鍵按一下 [dbo.Suppliers]。  
  
2.  選取 [檢視設計工具] 在資料表設計工具中檢視資料表結構描述。  
  
3.  選取 [Address] 資料行的 [允許 Null] 方塊。 請注意，指令碼窗格中對應的程式碼會立即變更為 `NULL`。  
  
4.  遵循[如何：使用 Power Buffer 更新連接的資料庫](../ssdt/how-to-update-a-connected-database-with-power-buffer.md)主題中的步驟更新資料庫。  
  
### <a name="to-populate-data-in-new-tables-using-a-transact-sql-query"></a>使用 Transact\-SQL 查詢在新資料表中填入資料  
  
1.  以滑鼠右鍵按一下 [Trade] 資料庫節點，再選取 [新增查詢]。  
  
2.  在指令碼窗格中，貼入下列程式碼。  
  
    ```  
    insert into dbo.Suppliers values  
    (1, 'NorthWind Traders', 'Seattle, WA'),  
    (2, 'Contoso', 'Tacoma, WA')  
    GO  
  
    insert dbo.Customer values  
    (1, 'Fourth Coffee')  
    GO  
  
    insert dbo.Products values  
    (1, 'Apples', 0, 1, 1),  
    (2, 'Instant Coffee', 1, 2, 1)  
    GO  
    ```  
  
3.  按一下 [執行查詢] 按鈕執行這個查詢。 [訊息] 窗格中的下列訊息指出資料列已成功加入至資料表。  
  
**(2 個資料列受影響)(1 個資料列受影響)(2 個資料列受影響)**  
  
4.  以下列程式碼取代指令碼窗格中的程式碼，並執行查詢。 這會嘗試使用 `Products` 為 6 將新資料列加入至 `ShelfLife` 資料表。  
  
    ```  
    insert dbo.Products values  
    (3, 'Potato Chips', 6, 1, 1)  
    GO  
    ```  
  
5.  [訊息] 窗格指出 `INSERT` 陳述式與現有的檢查條件約束 (將 `ShelfLife` 的值限制為低於 5) 相衝突。 沒有更新 Products 資料表，因為陳述式使現有的條件約束無效。  
  
6.  將程式碼變更為下列內容，並再次執行查詢。 請注意，這次的資料列更新成功。  
  
    ```  
    insert dbo.Products values  
    (3, 'Potato Chips', 2, 1, 1)  
    GO  
    ```  
  
## <a name="see-also"></a>另請參閱  
[管理資料表、關聯性及修正錯誤](../ssdt/manage-tables-relationships-and-fix-errors.md)  
[使用 Transact-SQL 編輯器，編輯及執行指令碼](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
