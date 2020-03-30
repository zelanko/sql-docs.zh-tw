---
title: 使用查詢建立新的資料庫物件
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: ac983ac7-f9c4-495d-8a99-e1ba370fb271
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 38a7165eb1145c6da08902d06a8483b0e26abf5b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241486"
---
# <a name="how-to-create-new-database-objects-using-queries"></a>如何：使用查詢建立新的資料庫物件

如果您想要使用指令碼建立或編輯檢視表、預存程序、函式、觸發程序或使用者定義型別，可以使用 Transact\-SQL 編輯器。 Transact\-SQL 編輯器提供了 IntelliSense 和其他語言支援。 如需詳細資訊，請參閱[使用 Transact-SQL 編輯器，編輯及執行指令碼](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)。  
  
使用 [檢視程式碼]\- **快顯功能表開啟連線的資料庫或專案中的資料庫實體時，會叫用 Transact**SQL 編輯器。 從 [SQL Server 物件總管] 使用 [新增查詢]  快顯功能表，或將新的指令碼物件加入至資料庫專案時，也會自動開啟這個編輯器。 如果您尚未連線到資料庫，但想要對它執行查詢，則也可以使用 [新增查詢連接]  對話方塊 (透過選取 [SQL]  功能表中的 [Transact-SQL 編輯器]  功能表)，連線到資料庫並啟動 Transact\-SQL 編輯器。  
  
> [!WARNING]  
> 下列程序將使用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)小節的程序中所建立的實體。  
  
### <a name="to-create-a-new-table-using-a-transact-sql-query"></a>使用 Transact\-SQL 查詢建立新的資料表  
  
1.  以滑鼠右鍵按一下 [Trade]  資料庫節點，再選取 [新增查詢]  。  
  
2.  在指令碼窗格中，貼入下列程式碼：  
  
    ```  
  
    CREATE TABLE [dbo].[Fruits] (  
        [Id]         INT NOT NULL,  
        [Perishable] BIT DEFAULT ((1)) NULL,  
        PRIMARY KEY CLUSTERED ([Id] ASC),  
        FOREIGN KEY ([Id]) REFERENCES [dbo].[Products] ([Id])   
    );  
    ```  
  
3.  按一下 Transact**SQL 編輯器工具列中的 [執行查詢]** \- 按鈕，執行這個查詢。  
  
4.  以滑鼠右鍵按一下 [SQL Server 物件總管]  中的 [Trade]  資料庫，然後選取 [重新整理]  。 請注意，新的 [Fruits]  資料表已經加入至資料庫。  
  
### <a name="to-create-a-new-function"></a>若要建立新的函式  
  
1.  用以下程式碼取代目前 Transact\-SQL 編輯器中的程式碼：  
  
    ```  
  
    CREATE FUNCTION [dbo].GetProductsBySupplier  
    (  
    @SupplierId int  
    )  
    RETURNS @returntable TABLE   
    (  
    [Id] int NOT NULL,   
    [Name] NVARCHAR (128) NOT NULL,  
    [Shelflife] INT NOT NULL,  
    [SupplierId] INT NOT NULL,  
    [CustomerId] INT NOT NULL  
    )  
    AS  
    BEGIN  
    INSERT @returntable  
    SELECT *  from Products p  
    where p.SupplierId = @SupplierId  
    RETURN   
    END  
    ```  
  
    這個函式會傳回 `Products` 資料表中所有 `SupplierId` 等於指定之參數的資料列。 按一下 Transact**SQL 編輯器工具列中的 [執行查詢]** \- 按鈕，執行這個查詢。  
  
2.  在 [SQL Server 物件總管] 中，於 [Trade]  節點底下，展開 [可程式性]  和 [函式]  節點。 您可以在 [資料表值函式]  底下找到剛才建立的新函式。  
  
### <a name="to-create-a-new-view"></a>建立新的檢視表  
  
1.  用以下程式碼取代目前 Transact\-SQL 編輯器中的程式碼。 然後，按一下編輯器上方的 [執行查詢]  按鈕，執行這個查詢。  
  
    ```  
    CREATE VIEW [dbo].PerishableFruits   
    AS SELECT p.Id, p.Name FROM dbo.Products p  
    join dbo.Fruits f on f.Id = p.Id  
    where f.Perishable = 1  
    ```  
  
2.  在 [SQL Server 物件總管] 中，於 [Trade]  節點底下，展開 [檢視]  節點以找出您剛才建立的新檢視。  
  
## <a name="see-also"></a>另請參閱  
[管理資料表、關聯性及修正錯誤](../ssdt/manage-tables-relationships-and-fix-errors.md)  
[使用 Transact-SQL 編輯器，編輯及執行指令碼](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
