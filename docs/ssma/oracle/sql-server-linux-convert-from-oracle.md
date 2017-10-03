---
title: "將 Oracle HR 結構描述移轉至 SQL Server on Linux |Microsoft 文件"
description: "範例 Oracle 結構描述轉換為 SQL Server on Linux"
author: edmacauley
ms.author: edmacauley
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: d49a98dd9268a2ea532b0b960bb0740580ccee69
ms.contentlocale: zh-tw
ms.lasthandoff: 10/02/2017

---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>將 Oracle 結構描述移轉至 SQL Server 2017 on Linux 與 SQL Server 移轉小幫手

此教學課程會使用 SQL Server 移轉小幫手 (SSMA) Windows 上的 Oracle 轉換 Oracle 範例**HR**結構描述以[Linux 上的 SQL Server 2017](../../linux/sql-server-linux-overview.md)。

> [!div class="checklist"]
> * 下載並安裝在 Windows 上的 SSMA
> * 建立 SSMA 專案，以管理移轉
> * 連接到 Oracle
> * 執行移轉報告
> * 範例 HR 結構描述轉換
> * 移轉資料

## <a name="prerequisites"></a>必要條件

- 執行個體的 Oracle 12c (12.2.0.1.0) 與**HR**安裝的結構描述
- 工作執行個體的 SQL Server on Linux

> [!NOTE]
> 目標 SQL Server 在 Windows 中，可以使用相同的步驟，但您必須選取在 Windows**移轉至**專案設定。

## <a name="download-and-install-ssma-for-oracle"></a>下載並安裝 SSMA for Oracle

根據來源資料庫，提供了數個版本的 SQL Server 移轉小幫手。  下載最新版[SQL Server 移轉小幫手 oracle](http://aka.ms/ssmafororacle)和下載頁面上的指示進行安裝。

> [!NOTE]
> 此時， **SSMA for Oracle 延伸模組組件**不支援 Linux，但它不需要在此教學課程。

## <a name="create-and-set-up-project"></a>建立和安裝專案

若要建立新的 SSMA 專案中使用下列步驟：

1. 開啟 SSMA for Oracle 並選擇 **新專案**從**檔案**功能表。

1. 指定專案的名稱。

1. 選擇 「 SQL Server 2017 (Linux)-Preview"**移轉至**欄位。

SSMA for Oracle 不使用預設的 Oracle 範例結構描述。 若要啟用 HR 結構描述，請使用下列步驟：

1. SSMA，在選取**工具**功能表。

1. 選取**預設專案設定**，然後選擇 **載入系統物件**。

1. 請確定**HR**已核取，然後選擇 **確定**。

## <a name="connect-to-oracle"></a>連接到 Oracle

接下來連接到 Oracle 的 SSMA。

1. 在工具列上，按一下  **Connect to Oracle**。

1. 輸入伺服器名稱、 連接埠、 Oracle SID、 使用者名稱和密碼。

   ![連接到 Oracle](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. 然後，按一下 [連接] 。 一段時間，SSMA for Oracle 連接至您的資料庫，並且讀取它的中繼資料。

## <a name="create-a-report"></a>建立報表

您可以使用下列步驟產生移轉報告。

1. 在**Oracle 中繼資料總管**，展開您的伺服器節點。

1. 展開**結構描述**，以滑鼠右鍵按一下**HR**，然後選取**建立報表**。

   ![Oracle 中繼資料總管 建立報表](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. 新的瀏覽器視窗開啟報表，其中會列出所有的警告和錯誤與轉換相關聯。

   > [!NOTE]
   > 您不需要執行任何動作清單在此教學課程。 如果您針對 Oracle 資料庫執行這些步驟，您應該檢閱報表以處理資料庫的所有重要的轉換問題。

   ![範例移轉報告](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>連接至 SQL Server

接下來選擇**連接到 SQL Server**並輸入適當的連接資訊。  如果您使用的資料庫名稱已經不存在，SSMA for Oracle 會為您建立它。

![連接至 SQL Server](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>轉換結構描述

以滑鼠右鍵按一下**HR**中**Oracle 中繼資料總管**，並選擇將轉換的結構描述。

![轉換結構描述](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>同步處理資料庫

接下來，同步處理您的資料庫。

1. 在轉換完成時，使用**SQL Server 中繼資料總管]**您先前步驟中，前往 [資料庫建立。

1. 以滑鼠右鍵按一下您在資料庫上，選取**同步處理資料庫**，然後按一下 [確定]。

   ![同步處理與資料庫](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>將資料移轉

最後一個步驟是將資料移轉。

1. 在**Oracle 中繼資料總管**，以滑鼠右鍵按一下**HR**，然後選取**移轉資料**。

1. 資料移轉步驟需要您重新輸入 Oracle 和 SQL Server 認證。

1. 完成後，請檢閱資料移轉報告，看起來應該類似下列的螢幕擷取畫面：

   ![資料移轉報告](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>後續的步驟

對於更複雜的 Orcale 結構描述中，轉換程序牽涉到更多時間、 測試和用戶端應用程式可能發生的變更。 本教學課程的用途是示範如何使用 SSMA for Oracle 整體的移轉程序的一部分。

在此教學課程中，您學會如何：
> [!div class="checklist"]
> * 在 Windows 上安裝 SSMA
> * 建立新的 SSMA 專案
> * 評估並執行從 Oracle 移轉

接下來，瀏覽使用 SSMA 其他方式：

> [!div class="nextstepaction"]
>[SQL Server 移轉小幫手的文件](../sql-server-migration-assistant.md)

