---
title: 使用資料表設計工具建立資料庫物件
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.design.table.scriptpanel
- sql.data.tools.design.table.context.view
ms.assetid: 9c9479c1-9bfc-4039-837e-e53fce67723d
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: ef475a7a0f5e2e8fdea510a0ee743f0d74d19dd2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75241497"
---
# <a name="how-to-create-database-objects-using-table-designer"></a>如何：使用資料表設計工具建立資料庫物件

[SQL Server 物件總管]  中新的 [SQL Server]  節點不僅看上去非常類似於 SSMS，還能讓您透過作用有如 SSMS 對應介面的關聯式功能表建立新物件。  
  
例如，您可以在 [資料庫]  節點底下建立新的資料庫。 您也可以選取特定的資料庫，然後使用新的資料表設計工具，快速建立或編輯資料表定義及其相關的程式設計物件。 從資料表設計工具中，您可以切換到指令碼窗格，讓您能夠直接編輯定義這個資料表的指令碼。  
  
### <a name="to-create-a-new-database"></a>若要建立新的資料庫  
  
1.  在 [SQL Server 物件總管]  中，展開 [SQL Server]  節點底下連接的伺服器執行個體。  
  
2.  以滑鼠右鍵按一下 [資料庫]  節點，再選取 [加入新的資料庫]  。  
  
3.  將新的資料庫重新命名為 **Trade**。  
  
### <a name="to-create-new-tables-using-the-table-designer"></a>若要使用資料表設計工具建立新的資料表  
  
1.  展開新建的 [Trade]  節點。 以滑鼠右鍵按一下 [資料表]  節點，再選取 [加入新的資料表]  。  
  
2.  資料表設計工具隨即在新視窗中開啟。 這個設計工具由資料行格線、指令碼窗格和內容窗格組成。 資料行格線會列出資料表中的所有資料行。 我們將在後面的程序再次討論這個設計工具的其他元件。  
  
3.  在指令碼窗格中將新的資料表重新命名為 `Suppliers`， 亦即將  
  
    ```  
    CREATE TABLE [dbo].[Table1]  
    ```  
  
    取代為  
  
    ```  
    CREATE TABLE [dbo].[Suppliers]  
    ```  
  
4.  在資料行格線中按一下空的資料列，將新的資料列加入資料表中。  分別為 [名稱]  和 [資料類型]  欄位輸入 **CompanyName** 和 **nvarchar (128)** ，並取消選取 [允許 Null]  欄位。 請注意，按 TAB 離開欄位時指令碼窗格會隨即更新。  
  
5.  加入其他新的資料行。 分別為 [名稱]  和 [資料類型]  欄位輸入 **Address** 和 **nvarchar (MAX)** ，並取消選取 [允許 Null]  欄位。  
  
    > [!WARNING]  
    > 從連接的資料庫編輯物件時，請不要將這些物件儲存到本機磁碟機。 若要將您的變更正確地儲存到資料庫，請遵循後續程序[如何：使用 Power Buffer 更新連接的資料庫](../ssdt/how-to-update-a-connected-database-with-power-buffer.md)中的步驟。  
  
6.  重複前面的步驟，建立另一個名為 **Customer** 的資料表。 這次使用資料行格線，將下列資料行加入至 Customer 資料表。 而且，記得要變更指令碼，讓資料表名稱為 `[dbo].[Customer]`。  
  
    |名稱|資料類型|**允許 Null**|  
    |--------|-------------|-------------------|  
    |Id|int|取消選取|  
    |名稱|nvarchar (128)|取消選取|  
  
7.  建立一個或多個名為 **Products** 的資料表。 使用資料行格線，將下列資料行加入至 Products 資料表。 而且，記得要變更指令碼，讓資料表名稱為 `[dbo].[Products]`。  
  
    |名稱|資料類型|**允許 Null**|  
    |--------|-------------|-------------------|  
    |Id|int|取消選取|  
    |名稱|nvarchar (128)|取消選取|  
    |ShelfLife|int|已選取|  
    |SupplierId|int|已選取|  
    |CustomerId|int|已選取|  
  
### <a name="to-create-a-new-check-constraint-using-the-table-designer"></a>若要使用資料表設計工具建立新的檢查條件約束  
  
1.  資料表設計工具的內容窗格提供資料表定義 (索引鍵、索引、條件約束、觸發程序等等) 的邏輯檢視，並讓您選取要反白顯示與個別資料行關聯性的物件。  
  
    針對 Products 資料表，在資料表設計工具的內容窗格中，以滑鼠右鍵按一下 [檢查條件約束]  節點，再選取 [加入新的檢查條件約束]  。  
  
2.  請注意，節點計數會自動遞增 1。  
  
3.  按一下指令碼窗格，以下列內容取代條件約束的預設定義。  
  
    ```  
    CONSTRAINT [CK_Products_ShelfLife] CHECK ([ShelfLife] <5),  
    ```  
  
    這個條件約束會將資料列的 ShelfLife 的值限制為低於 5。  
  
### <a name="to-create-new-foreign-key-references-using-the-table-designer"></a>若要使用資料表設計工具建立新的外部索引鍵參考  
  
1.  針對 Products 資料表，以滑鼠右鍵按一下內容窗格中的 [外部索引鍵]  ，再選取 [加入新的外部索引鍵]  。  
  
2.  請注意，節點計數會自動遞增 1。  
  
3.  按一下指令碼窗格，以下列內容取代外部索引鍵參考的預設定義。  
  
    ```  
    CONSTRAINT [FK_Products_SupplierId] FOREIGN KEY ([SupplierId]) REFERENCES [dbo].[Suppliers] ([Id]),  
    ```  
  
4.  重複前面的步驟，將另一個外部索引鍵參考加入至 Products 資料表。 這次以下列內容取代預設定義。  
  
    ```  
    CONSTRAINT [FK_Products_CustomerId] FOREIGN KEY ([CustomerId]) REFERENCES [dbo].[Customer] ([Id])  
    ```  
  
## <a name="see-also"></a>另請參閱  
[管理資料表、關聯性及修正錯誤](../ssdt/manage-tables-relationships-and-fix-errors.md)  
  
