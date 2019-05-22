---
title: 如何：刪除物件及解析相依性 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Data.Tools.Project.HelpKeywords.SqlProjectDropDatabaseConfirmationDialog
- sql.data.tools.dropdatabaseconfirmation.dialog
- sql.data.tools.dropmultipledatabasesconfirmation.dialog
ms.assetid: fb31c2b1-ca4f-4e11-a0b6-5c26430f1c8c
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: cd4b8ab01b2b9f16938e9493d5e762cae59a6446
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65090209"
---
# <a name="how-to-delete-objects-and-resolve-dependencies"></a>如何：刪除物件及解析相依性
在 [SQL Server 物件總管] 中重新命名或刪除物件時，SQL Server Data Tools 會自動偵測該物件的所有相依性物件，並視需要準備 ALTER 指令碼以重新命名或卸除相依性。  
  
> [!WARNING]  
> 下列程序將使用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)小節的程序中所建立的實體。  
  
### <a name="to-delete-a-database"></a>若要刪除資料庫  
  
1.  以滑鼠右鍵按一下 [SQL Server 物件總管] 中的 資料庫，然後選取 [刪除]。  
  
2.  接受 [刪除資料庫] 對話方塊中的所有預設值，然後按一下 [確定]。  
  
### <a name="to-rename-a-table"></a>重新命名資料表  
  
1.  確定 `Customer` 資料表未在資料表設計工具或 Transact\-SQL 編輯器中開啟。  
  
2.  在 [SQL Server 物件總管] 中展開 [資料表] 節點。 以滑鼠右鍵按一下 [Customer] 資料表，再選取 [重新命名]。  
  
3.  將資料表名稱變更為 **Customers**，然後按 ENTER。  
  
4.  請注意，系統會立即替您叫用 [資料庫更新] 作業。 SSDT 會替您呼叫 sp_rename 預存程序來重新命名資料表。 如果有任何的相依物件 (如外部索引鍵條件約束)，也會一併進行更新。  
  
    > [!WARNING]  
    > SSDT 不會自動更新以指令碼為主的相依性 (如從檢視表至資料表的參考) 或預存程序。 在重新命名之後，您可以使用 [錯誤清單] 窗格尋找所有其他相依性，再手動加以修正。  
  
5.  遵循先前[如何：使用 Power Buffer 更新連線的資料庫](../ssdt/how-to-update-a-connected-database-with-power-buffer.md)程序中的步驟套用變更。  
  
6.  再次以滑鼠右鍵按一下 [SQL Server 物件總管] 中的 [Customers] 資料表，然後選取 [檢視資料]。 請注意，在重新命名作業之後資料表資料完整無損。  
  
7.  以滑鼠右鍵按一下 [Products] 資料表，再選取 [檢視程式碼]。 請注意，外部索引鍵參考已經自動更新為 `REFERENCES [dbo].[Customers] ([Id])`，以反映重新命名作業。  
  
### <a name="to-delete-a-table"></a>若要刪除資料表  
  
1.  以滑鼠右鍵按一下 [SQL Server 物件總管] 中的 [Customers] 資料表，然後選取 [刪除]。  
  
2.  請注意，在 [預覽資料庫更新] 對話方塊的 [使用者動作] 區段底下，SSDT 已識別出所有的相依物件，因此將會卸除外部索引鍵參考。  
  
3.  按一下 [更新資料庫]。  
  
4.  以滑鼠右鍵按一下 [SQL Server 物件總管] 中的 [Products] 資料表，然後選取 [檢視程式碼]。 請注意，`Customers` 資料表的外部索引鍵參考已不存在。  
  
    > [!WARNING]  
    > 刪除作業發生時，如果已在資料表設計工具或 Transact\-SQL 編輯器中開啟 [Products] 資料表，後者不會自動重新整理以顯示外部索引鍵參考的刪除。 此外，在 [錯誤清單] 中可能會顯示和無法解析的參考有關的錯誤。 若要解決此問題，請關閉資料表設計工具或 Transact\-SQL 編輯器，再重新開啟 [Products] 資料表。  
  
