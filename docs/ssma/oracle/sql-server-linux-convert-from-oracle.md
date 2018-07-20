---
title: 將 Oracle HR 結構描述移轉至 Linux 上的 SQL Server |Microsoft Docs
description: 將範例 Oracle 結構描述轉換成 SQL Server on Linux
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.suite: sql
ms.custom: ''
ms.technology: ssma
ms.openlocfilehash: 9a556b8b800a03808def02c2953107faa90d7e34
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086070"
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>Oracle 結構描述移轉至 SQL Server 2017 Linux 上使用 SQL Server 移轉小幫手

本教學課程使用 SQL Server Migration Assistant (SSMA) for Windows 上的 Oracle 轉換 Oracle 範例**HR**結構描述[Linux 上的 SQL Server 2017](../../linux/sql-server-linux-overview.md)。

> [!div class="checklist"]
> * 下載並安裝在 Windows 上的 SSMA
> * 建立 SSMA 專案來管理移轉
> * 連接到 Oracle
> * 執行移轉報告
> * 將轉換的範例 HR 結構描述
> * 將資料移轉

## <a name="prerequisites"></a>先決條件

- 執行個體的 Oracle 12c (12.2.0.1.0) 與**HR**安裝的結構描述
- Linux 上的 SQL Server 的工作執行個體

> [!NOTE]
> 可以使用相同的步驟，以目標 SQL Server on Windows，但您必須選取中的 Windows**移轉至**專案設定。

## <a name="download-and-install-ssma-for-oracle"></a>下載並安裝 SSMA for Oracle

另外還有數個版本的 SQL Server Migration Assistant，根據您的來源資料庫。  下載最新版[SQL Server Migration Assistant for Oracle](http://aka.ms/ssmafororacle)和使用的下載頁面上找到的指示進行安裝。

> [!NOTE]
> 在此階段中， **SSMA for Oracle 延伸模組組件**不支援在 Linux 上，但它不需要在此教學課程。

## <a name="create-and-set-up-project"></a>建立和設定專案

若要建立新的 SSMA 專案中使用下列步驟：

1. 開啟 SSMA for Oracle，然後選擇**新的專案**從**檔案**功能表。

1. 指定專案的名稱。

1. 選擇 「 SQL Server 2017 (Linux)-預覽 」 中**移轉至**欄位。

SSMA for Oracle 不會使用預設的 Oracle 範例結構描述。 若要啟用 HR 結構描述，請使用下列步驟：

1. SSMA 中，選取**工具**功能表。

1. 選取 **預設專案設定**，然後選擇**載入系統物件**。

1. 請確定**HR**勾選，然後選擇**確定**。

## <a name="connect-to-oracle"></a>連接到 Oracle

接著連接到 Oracle 的 SSMA。

1. 在工具列上，按一下**連接到 Oracle**。

1. 輸入伺服器名稱、 連接埠、 Oracle SID、 使用者名稱和密碼。

   ![連接到 Oracle](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. 然後，按一下 [連接] 。 幾分鐘後，SSMA for Oracle 連線到您的資料庫，並讀取其中繼資料。

## <a name="create-a-report"></a>建立報表

您可以使用下列步驟來產生移轉報告。

1. 在 [ **Oracle 中繼資料總管]**，展開您的伺服器節點。

1. 依序展開**結構描述**，以滑鼠右鍵按一下**HR**，然後選取**建立報表**。

   ![Oracle 中繼資料總管 建立報表](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. 新的瀏覽器視窗開啟報表，其中會列出所有與轉換相關聯的錯誤與警告。

   > [!NOTE]
   > 您不需要進行任何動作的清單在本教學課程。 如果您針對 Oracle 資料庫執行這些步驟，您應該檢閱報表以處理資料庫的所有重要的轉換問題。

   ![範例移轉報告](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>連接至 SQL Server

接下來選擇**連接到 SQL Server**並輸入適當的連接資訊。  如果您使用的資料庫名稱已經不存在，SSMA for Oracle 則會為您建立它。

![連接至 SQL Server](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>將結構描述轉換

以滑鼠右鍵按一下**HR**中**Oracle 中繼資料總管**，然後選擇將轉換的結構描述。

![將結構描述轉換](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>同步處理資料庫

接下來，同步處理您的資料庫。

1. 在轉換完成時，使用**SQL Server 中繼資料總管]** 您在上一個步驟中移至 [資料庫建立。

1. 以滑鼠右鍵按一下您在資料庫上，選取**同步處理資料庫**，然後按一下 [確定]。

   ![同步處理與資料庫](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>將資料移轉

最後一個步驟是將資料移轉。

1. 中**Oracle 中繼資料總管**，以滑鼠右鍵按一下**HR**，然後選取**移轉資料**。

1. 資料移轉步驟需要您重新輸入您的 Oracle 和 SQL Server 認證。

1. 完成時，檢閱資料移轉報告，看起來應該類似下列螢幕擷取畫面：

   ![資料移轉報告](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>後續步驟

針對更複雜的 Orcale 結構描述中，轉換程序牽涉到更多時間、 測試和用戶端應用程式可能發生的變更。 本教學課程的目的是示範如何使用 SSMA for Oracle 整體移轉程序的一部分。

在本教學課程中，您已了解如何：
> [!div class="checklist"]
> * Windows 上安裝 SSMA
> * 建立新的 SSMA 專案
> * 評估並從 Oracle 執行移轉

接下來，瀏覽其他 SSMA 使用方式：

> [!div class="nextstepaction"]
>[SQL Server Migration Assistant 的文件](../sql-server-migration-assistant.md)
