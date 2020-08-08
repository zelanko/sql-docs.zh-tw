---
title: 將 Oracle HR 架構遷移至 Linux 上的 SQL Server |Microsoft Docs
description: 將範例 Oracle 架構轉換成 Linux 上的 SQL Server
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: ssma
ms.openlocfilehash: 1d28458896d4ae4806db1b0f705c5e33badddfb7
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932749"
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>使用 SQL Server 移轉小幫手將 Oracle 架構遷移至 Linux 上的 SQL Server 2017

本教學課程使用 SQL Server 移轉小幫手 (SSMA) for Oracle on Windows，將 Oracle 範例**HR**架構轉換成[Linux 上的 SQL Server 2017](../../linux/sql-server-linux-overview.md)。

> [!div class="checklist"]
> * 在 Windows 上下載並安裝 SSMA
> * 建立 SSMA 專案以管理遷移
> * 連接到 Oracle
> * 執行遷移報告
> * 轉換範例 HR 架構
> * 移轉資料

## <a name="prerequisites"></a>必要條件

- 已安裝**HR**架構的 Oracle 12c (12.2.0.1.0) 實例
- Linux 上的 SQL Server 的工作實例

> [!NOTE]
> 相同的步驟可以用來將 Windows 上的 SQL Server 設為目標，但您必須在 [**遷移至**專案] 設定中選取 [Windows]。

## <a name="download-and-install-ssma-for-oracle"></a>下載並安裝 SSMA for Oracle

根據您的源資料庫而定，有數個可用的 SQL Server 移轉小幫手版本。  下載 Oracle 目前版本的 SQL Server 移轉小幫手，並使用下載頁面上找到的指示[來進行](https://aka.ms/ssmafororacle)安裝。

> [!NOTE]
> 目前 Linux 不支援**SSMA For Oracle 延伸模組套件**，但本教學課程不需要此功能。

## <a name="create-and-set-up-project"></a>建立和設定專案

使用下列步驟來建立新的 SSMA 專案：

1. 開啟 SSMA for Oracle，然後從 [檔案]**功能表中選擇 [** **新增專案**]。

1. 將專案命名。

1. 在 [**遷移至**] 欄位中選擇 [SQL Server 2017 (Linux) -預覽]。

SSMA for Oracle 預設不會使用 Oracle 範例架構。 若要啟用 HR 架構，請使用下列步驟：

1. 在 SSMA 中，選取 [**工具**] 功能表。

1. 選取 [**預設專案設定**]，然後選擇 [**載入系統物件**]。

1. 請確定已核取 [ **HR** ]，然後選擇 **[確定]**。

## <a name="connect-to-oracle"></a>連接到 Oracle

接下來，將 SSMA 連接到 Oracle。

1. 在工具列上，按一下 [**連接到 Oracle]**。

1. 輸入 [伺服器名稱]、[埠]、[Oracle SID]、[使用者名稱] 和 [密碼]。

   ![連接到 Oracle](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. 然後按一下 [ **連接**]。 幾分鐘後，SSMA for Oracle 就會連接到您的資料庫並讀取其中繼資料。

## <a name="create-a-report"></a>建立報表

使用下列步驟來產生遷移報表。

1. 在 [ **Oracle 中繼資料瀏覽器**] 中，展開伺服器的節點。

1. 展開 [**架構**]，以滑鼠右鍵按一下 [ **HR**]，然後選取 [**建立報告**]。

   ![Oracle Metadata Explorer 建立報表](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. 新的瀏覽器視窗隨即開啟，其中會列出與轉換相關聯的所有警告和錯誤。

   > [!NOTE]
   > 您不需要在本教學課程中使用該清單執行任何動作。 如果您針對自己的 Oracle 資料庫執行這些步驟，您應該檢查報告以解決資料庫的任何重要轉換問題。

   ![範例遷移報表](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>連接至 SQL Server

接下來，選擇 [**連接到 SQL Server]** ，然後輸入適當的連接資訊。  如果您使用尚未存在的資料庫名稱，SSMA for Oracle 就會為您建立。

![連接至 SQL Server](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>轉換結構描述

以滑鼠右鍵按一下**Oracle Metadata Explorer**中的 [ **HR** ]，然後選擇 [轉換架構]。

![轉換結構描述](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>同步處理資料庫

接下來，同步處理您的資料庫。

1. 轉換完成後，請使用 SQL Server 的**中繼資料瀏覽器**，移至您在上一個步驟中建立的資料庫。

1. 以滑鼠右鍵按一下您的資料庫，選取 [**與資料庫同步處理**]，然後按一下 [確定]。

   ![與資料庫同步處理](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>移轉資料

最後一個步驟是遷移您的資料。

1. 在 [ **Oracle 中繼資料瀏覽器**] 中，以滑鼠右鍵按一下 [ **HR**]，然後選取 [**遷移資料**]。

1. 資料移轉步驟會要求您重新輸入 Oracle 和 SQL Server 認證。

1. 完成時，請檢查資料移轉報告，其看起來應該類似下列螢幕擷取畫面：

   ![資料移轉報告](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>後續步驟

針對更複雜的 Orcale 架構，轉換程式會牽涉到更多的時間、測試和可能變更的用戶端應用程式。 本教學課程的目的是要說明如何在整體遷移程式中使用 SSMA for Oracle。

在本教學課程中，您已了解如何：
> [!div class="checklist"]
> * 在 Windows 上安裝 SSMA
> * 建立新的 SSMA 專案
> * 評估並執行 Oracle 的遷移

接下來，探索其他使用 SSMA 的方式：

> [!div class="nextstepaction"]
>[SQL Server 移轉小幫手檔](../sql-server-migration-assistant.md)
