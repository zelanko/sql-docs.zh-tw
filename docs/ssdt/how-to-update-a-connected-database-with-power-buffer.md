---
title: 使用 Power Buffer 更新連線的資料庫
description: 了解如何使用 Power Buffer 來更新資料庫。 請參閱如何在套用變更之前先驗證變更，以及如何在指令碼中儲存變更，以供日後部署。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.commitpreview.dialog
ms.assetid: 4048b7f8-71a9-47ad-b812-3fc1e8066240
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 3954ae84a201209e49b65dc421ab41b93126fb65
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893868"
---
# <a name="how-to-update-a-connected-database-with-power-buffer"></a>如何：使用 Power Buffer 更新連線的資料庫

SQL Server Data Tools Power Buffer 技術讓您可以輕易地儲存目前工作階段的所有編輯，以套用對連接的資料庫所做的變更。 在 Power Buffer 視窗 (如 Transact\-SQL 編輯器或資料表設計工具) 中編輯所造成的任何錯誤會立即顯示在 [錯誤清單]**** 窗格，這可讓您追蹤識別的錯誤以進行進一步疑難排解。 您可以驗證暫止變更，直到準備好將其套用到資料庫為止。 在進行更新程序期間，SSDT 會依據您的編輯來自動建立 ALTER 指令碼，並提醒您注意任何可能發生的問題。 然後，您可以將所有開啟中 Power Buffer 視窗至今累積的一切變更套用到相同資料庫，或是儲存 ALTER 指令碼以供日後部署。  
  
SSDT 也會分辨在 Visual Studio 之外對資料庫結構描述所做的變更。 例如，如果您在 SQL Server Management Studio 中加入新資料表至現有資料庫，此類變更會立即顯示在 Visual Studio 的 SQL Server 物件總管中，而不必由您手動重新整理。 此一漂移偵測功能可確保您在 SQL Server 物件總管中看到的永遠是資料庫最新的結構描述定義。 請注意，任何在資料表設計工具或 Transact\-SQL 編輯器中開啟以進行編輯的資料庫物件，將不會重新整理以顯示 Visual Studio 之外的變更。  
  
下列程序將利用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)小節的程序中所建立的實體。  
  
### <a name="to-apply-the-changes-made-in-the-previous-procedures"></a>若要套用先前的程序所做的變更  
  
1.  按一下工具列上的綠色 [更新] 按鈕 (如果您將滑鼠游標停留在該按鈕上方，就會顯示「更新資料庫」工具提示)。 工具列位於資料表設計工具的資料行格線上。  
  
2.  [預覽資料庫更新] 對話方塊隨即出現。 在背景會產生以您所做的變更為基礎的部署指令碼。 這個對話方塊接著會顯示 SSDT 即將採取的動作 (例如建立或卸除資料庫實體) 摘要，以及其已識別的可能發生的問題 (這不適用於我們的程序，但在資料庫定義包含錯誤，而必須先解決此錯誤才能更新的時候會用到)。  
  
3.  如果目前不想要更新資料庫，請按一下 [取消]**** 按鈕以結束 [預覽資料庫更新]**** 對話方塊。  
  
4.  如果到目前為止對變更相當滿意，請按一下 [預覽資料庫更新] 對話方塊中的 [更新資料庫] 按鈕。 系統會替您執行部署指令碼，而累積的變更現在會套用到資料庫。  
  
5.  如果您要檢視部署指令碼以進行確認，或要在更新前進行一些變更，請按一下 [預覽資料庫更新]**** 對話方塊中的 [產生指令碼]**** 按鈕。 產生的指令碼會在新的 Transact\-SQL 編輯器視窗中開啟。 您可以按下 Transact\-SQL 編輯器工具列上的 [執行查詢] 按鈕以執行這個查詢。 這與步驟 4 中 [更新資料庫] 按鈕所做的動作類似。  
  
    > [!WARNING]  
    > 如果對部署指令碼進行任何變更後再加以執行，這種變更並不會顯示在任何已開啟的資料庫實體中。 例如，如果在部署指令碼中重新命名 `Customers` 資料表的資料行並加以執行以更新資料庫，但 `Customers` 資料表已在資料表設計工具中開啟的話，則按下 [更新資料庫]**** 按鈕後該資料行名稱仍會是舊名稱。 您必須手動關閉資料表設計工具，而不在本機另存為指令碼。 從 [SQL Server 物件總管]**** 再次開啟資料表時，您會發現資料庫會以您在部署指令碼中所做的變更來更新。  
  
6.  在 Transact\-SQL 編輯器的 [輸出]**** 窗格 (如果您自行執行部署指令碼則為 [訊息]**** 窗格) 中，請注意下列表示更新成功的訊息。  
  
**正在建立 [dbo].[Customers]... 正在建立 [dbo].[Products]... 正在建立 [dbo].[Suppliers]... 正在建立 FK_Products_SupplierId... 正在建立 FK_Products_CustomerId... 正在建立 CK_Products_ShelfLife。資料庫更新的異動部分成功。正在針對新建立的條件約束檢查現有資料。更新完成。**  
  
7.  在 [SQL Server 物件總管] 中，請注意新資料表已經顯示在 [Trade] 資料庫的 [資料表] 節點底下。  
  
### <a name="to-view-changes-made-to-a-database-outside-visual-studio"></a>若要在 Visual Studio 之外檢視對資料庫所做的變更  
  
1.  開啟 SQL Server Management Studio。 在 [連接到伺服器]**** 對話方塊中，輸入您在 Visual Studio 中已經連接的相同資料庫伺服器，然後按一下 [連接]****。  
  
2.  在 [SQL Server 物件總管] 中，展開 [資料庫] 並巡覽至 [Trade] 資料庫。  
  
3.  以滑鼠右鍵按一下 [Trade] 底下的 [資料表]，再選取 [新增資料表]。 在資料表設計工具中，輸入 **id** 做為資料行名稱，並輸入**int** 做為資料類型。  
  
4.  按一下工具列中的 [儲存] 圖示儲存資料表。 接受預設名稱，並按一下 [確定]。  
  
    回到 Visual Studio。 在 [SQL Server 物件總管] 中，檢查 [Trade] 資料庫底下的 [資料表] 節點。 請注意新建的 [Table_1] 資料表的外觀。  
  
5.  以滑鼠右鍵按一下 [Table_1]，再選取 [刪除]。 按一下 [預覽資料庫更新] 對話方塊中的 [更新資料庫]。  
  
## <a name="see-also"></a>另請參閱  
[操作說明：修正錯誤](../ssdt/how-to-fix-errors.md)  
  
