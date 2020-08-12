---
title: 建置及部署至本機資料庫
description: 了解 SQL Server 2012 所提供的本機伺服器執行個體。 了解如何使用此執行個體來建置、測試及偵錯開發專案。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: ebca8ff8-9a09-4207-8979-9d577af7c1d5
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: d7503049f0ea68b38206764eb3163a5a80a0b2d7
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/29/2020
ms.locfileid: "85518918"
---
# <a name="how-to-build-and-deploy-to-a-local-database"></a>如何：建置及部署至本機資料庫

Microsoft SQL Server 2012 提供本機指定的伺服器執行個體，稱為 SQL Server Express 本機資料庫執行階段，在偵錯 SQL Server 資料庫專案時會啟動這個執行個體。 這個本機伺服器執行個體可做為建置、測試及偵錯專案的沙箱。 它獨立於任何已安裝的 SQL Server 執行個體，而且無法從 SQL Server Data Tools (SSDT) 外部存取。 這種配置適用於有限存取或無法存取生產資料庫，但想要在授權人員將專案部署到生產環境之前先在本機測試專案的開發人員。 此外，開發 SQL Azure 的資料庫方案時，您可以利用這個本機伺服器的便利性，先在本機開發及測試資料庫專案，再將其部署至雲端上。  
  
> [!WARNING]  
> 在 [SQL Server 物件總管] 中於本機資料庫節點底下的資料庫，是其對應的資料庫專案的反射，與連接的伺服器執行個體中同名的資料庫無關。  
  
> [!WARNING]  
> 下列程序利用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)和[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)小節中的程序所建立的實體。  
  
### <a name="to-use-the-local-database"></a>若要使用本機資料庫  
  
1.  請注意，在 [SQL Server 物件總管] 的 [SQL Server] 節點下，出現名稱為 [本機] 的新節點。 這是本機資料庫執行個體。  
  
2.  展開 [本機] 和 [資料庫] 節點。 請注意，出現與 TradeDev 專案同名的資料庫。 展開這個資料庫底下的節點。 [資料工具作業] 視窗隨即顯示 [本機] 節點下任何資料庫展開/匯入作業的進度狀態。 請注意，這些節點不包含我們在先前的程序中所建立的任何資料表和實體。  
  
3.  按 F5 偵錯 TradeDev 資料庫專案。  
  
    SSDT 預設會使用本機資料庫伺服器執行個體來偵錯資料庫專案。 在這種情況下，SSDT 會先嘗試建置專案，若沒有發生錯誤，則會將專案 (及其實體) 部署到本機資料庫。 如果之後偵錯相同的專案，SSDT 會先偵測上次偵錯之後的任何變更，然後只將那些變更部署到本機資料庫。  
  
4.  重新展開 [本機] 資料庫伺服器中 [TradeDev] 底下的節點。 這次請注意，資料表、檢視表和函式已經部署到本機資料庫伺服器。  
  
5.  以滑鼠右鍵按一下 [TradeDev] 節點，再選取 [新增查詢]。  
  
6.  在指令碼窗格中，貼上下列程式碼，再按一下 [執行查詢] 按鈕執行這個查詢。  
  
    ```  
    select * from dbo.GetProductsBySupplier(1)  
    ```  
  
7.  [訊息] 窗格顯示「(0 個資料列受影響)」，而 [結果] 窗格沒有傳回任何資料列。 這是因為我們查詢的是本機資料庫，而不是真正包含實際資料的連接資料庫。  
  
    您可以以滑鼠右鍵按一下這個本機 [TradeDev] 資料庫底下的 [Products] 資料表，再選取 [檢視資料] 來確認。 請注意，這個資料表是空的。  
  
### <a name="to-replicate-real-data-to-the-local-database"></a>若要將實際資料複寫到本機資料庫  
  
1.  在 [SQL Server 物件總管]，展開您的已連接 SQL Server 執行個體並找出 [TradeDev] 資料庫。  
  
    以滑鼠右鍵按一下 [Suppliers] 資料表，再選取 [檢視資料]。  
  
2.  按一下資料編輯器上方的 [指令碼] 按鈕 (右邊數來第二個按鈕)。 從指令碼複製 `INSERT` 陳述式。  
  
3.  展開 [本機] 伺服器執行個體，然後以滑鼠右鍵按一下 [TradeDev] 節點，再選取 [新增查詢]。  
  
4.  將 `INSERT` 陳述式貼入這個查詢視窗並執行查詢。  
  
5.  重複前面的步驟，將資料從連接的 [TradeDev] 資料庫中的 [Products] 和 [Fruits] 資料表複寫到本機 [TradeDev] 資料庫。  
  
6.  以滑鼠右鍵按一下 [本機] 伺服器執行個體，再選取 [重新整理]。 使用 [檢視資料] 檢查資料表，以驗證本機資料庫已擴展。  
  
7.  以滑鼠右鍵按一下本機伺服器執行個體的 [TradeDev] 節點，再選取 [新增查詢]。  
  
8.  在指令碼窗格中，貼上下列程式碼，再按一下 [執行查詢] 按鈕執行這個查詢。  
  
    ```  
    select * from dbo.GetProductsBySupplier(1)  
    ```  
  
9. 在 Transact\-SQL 編輯器窗格下方的 [結果]**** 窗格中，您會看到傳回 `Products` 資料表的 Apples 和 Potato Chips 資料列。  
  
