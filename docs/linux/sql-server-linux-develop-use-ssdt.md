---
title: 開發和部署適用於 Linux 的 SQL Server 資料庫  | Microsoft Docs
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.openlocfilehash: c6d5789092ea2bbfc6fd9a8bb20cc7d078eaf6de
ms.sourcegitcommit: c4258a644ac588fc222abee2854f89a81325814c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/17/2019
ms.locfileid: "72545051"
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>使用 Visual Studio 建立 Linux 的 SQL Server 資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server Data Tools (SSDT) 可將 Visual Studio 轉化為適用於 Linux SQL Server 的強大開發和資料庫生命週期管理 (DLM) 環境。 您可以從原始檔控制的專案中來開發、建置、測試及發佈資料庫。 如同開發應用程式程式碼一樣。

## <a name="install-visual-studio-and-sql-server-data-tools"></a>安裝 Visual Studio 和 SQL Server Data Tools

1. 如果您尚未在 Windows 電腦上安裝 Visual Studio，請[下載並安裝 Visual Studio](https://visualstudio.microsoft.com/downloads/)。 如果沒有 Visual Studio 授權，則 Visual Studio Community 版本是功能完整的 IDE，供學生、開放原始碼和個人開發人員免費使用。

2. 在 Visual Studio 安裝期間，請針對 [選擇安裝類型]  選項選取 [自訂]  。 按 **[下一步]**

3. 從功能選取清單中，選取 [Microsoft SQL Server Data Tools]、[Git for Windows] 和 [Visual Studio 的 GitHub 延伸模組]。   

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. 繼續並完成安裝 Visual Studio。 這可能需要幾分鐘的時間。

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>將 SQL Server Data Tools 升級至 SSDT 17.0 RC 版本

SSDT 17.0 RC 或更新版本支援 Linux 上的 SQL Server。

* [下載並安裝 SSDT 17.0 RC2](https://go.microsoft.com/fwlink/?linkid=837939)。

## <a name="create-a-new-database-project-in-source-control"></a>建立由原始檔控制的新資料庫專案

1. 啟動 Visual Studio。

2. 在 [檢視]  功能表上，選取 **Team Explorer**。 

3. 在 [連線]  頁面上，按一下 [本機 Git 存放庫]  區段中的 [新增]  。

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. 按一下 **[建立]** 。 建立本機 Git 存放庫之後，請按兩下 **SSDTRepo**。

4. 按一下 [解決方案]  區段中的 [新增]  。 在 [新增專案]  對話方塊中，選取 [其他語言]  節點下的 [SQL Server]  。

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. 鍵入 **TutorialDB** 名稱，然後按一下 [確定]  以建立新的資料庫專案。

## <a name="create-a-new-table-in-the-database-project"></a>在資料庫專案中，建立新的資料表

1. 在 [檢視]  功能表上，選取 [方案總管]  。

2. 以滑鼠右鍵按一下 [方案總管] 中的 **TutorialDB**，以開啟資料庫專案功能表。

3. 選取 [新增]  底下的 [資料表]  。

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. 使用資料表設計工具，新增「名稱 `nvarchar(50)`」和「位置 `nvarchar(50)`」這兩個資料行，如下圖所示。 當您在設計工具中新增資料行時，SSDT 會產生 `CREATE TABLE` 指令碼。

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. 儲存 **Table1.sql** 檔案。

## <a name="build-and-validate-the-database"></a>建置和驗證資料庫

1. 開啟 **TutorialDB** 上的資料庫專案功能表，然後選取 [建置]  。 SSDT 會編譯專案中的 .sql 原始程式碼檔案，並建置資料層應用程式套件 (dacpac) 檔案。 這可用來將資料庫發佈至 Linux 上的 SQL Server 執行個體。 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. 在 Visual Studio 中，查看 [輸出]  視窗的建置成功訊息。 

## <a name="publish-the-database-to-sql-server-instance-on-linux"></a>將資料庫發佈至 Linux 上的 SQL Server 執行個體

1. 開啟 **TutorialDB** 上的資料庫專案功能表，然後選取 [發佈]  。

2. 按一下 [編輯]  ，選取 Linux 上的 SQL Server 執行個體。

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. 在連線對話方塊中，鍵入 Linux 上 SQL Server 執行個體的 IP 位址或主機名稱、使用者名稱和密碼。

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. 按一下發佈對話方塊上的 [發佈]  按鈕。

5. 查看 [資料工具作業]  視窗中的發佈狀態。

6. 按一下 [檢視結果]  或 [檢視指令碼]  ，以查看 Linux 上的 SQL Server 資料庫發佈結果詳細資料。

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

您已成功在 Linux 上的 SQL Server 執行個體建立新資料庫，並了解使用原始檔所控制資料庫專案來開發資料庫的基本概念。

## <a name="next-steps"></a>後續步驟

如果您不熟悉 T-SQL，請參閱[教學課程：撰寫 Transact-SQL 陳述式](../t-sql/tutorial-writing-transact-sql-statements.md)。

如需使用 SQL Data Tools 開發資料庫的詳細資訊，請參閱下列文章。

* [下載及安裝 Visual Studio](https://www.visualstudio.com/downloads/)
* [下載並安裝 SSDT](https://aka.ms/ssdt-download)
* [SSDT MSDN 文件](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)
* [教學課程：撰寫 Transact-SQL 陳述式](https://msdn.microsoft.com/library/ms365303.aspx)
* [Transact-SQL 參考 (資料庫引擎)](https://msdn.microsoft.com/library/bb510741.aspx)
