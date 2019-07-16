---
title: 開發和部署 SQL Server 資料庫的 Linux |Microsoft Docs
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.openlocfilehash: b98980837f6dce2ebd9f39be142b816f37f16cd8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077397"
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>使用 Visual Studio 來建立 Linux 上的 SQL Server 資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Linux 上的 SQL Server，SQL Server Data Tools (SSDT) 會將 Visual Studio 變成強大的開發和資料庫生命週期管理 (DLM) 環境。 您可以開發、 建置、 測試及發佈您的資料庫從原始檔控制的專案，就像開發應用程式程式碼。

## <a name="install-visual-studio-and-sql-server-data-tools"></a>安裝 Visual Studio 和 SQL Server Data Tools

1. 如果您未在您的 Windows 電腦上已安裝 Visual Studio[下載並安裝 Visual Studio]。 如果您沒有 Visual Studio 授權，Visual Studio Community edition 是免費、 功能完整的 IDE，適用於學生、 開放原始碼及個人開發人員。

2. 在 Visual Studio 安裝中，選取**自訂**for**選擇 安裝類型**選項。 按 **[下一步]**

3. 選取**Microsoft SQL Server Data Tools**， **Git for Windows**，並**Visual Studio 的 GitHub 延伸模組**從 功能選取項目清單。

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. 繼續並完成 Visual Studio 的安裝。 可能需要幾分鐘的時間。

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>升級至 SSDT 17.0 RC 版本的 SQL Server Data Tools

SSDT 17.0 RC 或更新版本的版本支援在 Linux 上的 SQL Server。

* [下載和安裝 SSDT 17.0 RC2](https://go.microsoft.com/fwlink/?linkid=837939)。

## <a name="create-a-new-database-project-in-source-control"></a>在 原始檔控制中建立新的資料庫專案

1. 啟動 Visual Studio。

2. 選取  **Team Explorer**上**檢視**功能表。 

3. 按一下 **的新**中**本機 Git 儲存機制**區段**Connect**頁面。

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. 按一下 [建立]  。 建立本機 Git 存放庫之後，按兩下**SSDTRepo**。

4. 按一下 **的新**中**解決方案**一節。 選取  **SQL Server**下方**其他語言**節點中的**新專案**對話方塊。

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. 在中輸入**TutorialDB**的名稱，然後按一下**確定**來建立新的資料庫專案。

## <a name="create-a-new-table-in-the-database-project"></a>資料庫專案中建立新的資料表

1. 選取 **方案總管**上**檢視**功能表。

2. 開啟資料庫的 專案 功能表上按一下滑鼠右鍵**TutorialDB**方案總管 中。

3. 選取 **表格**下方**新增**。

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. 使用資料表設計工具中，新增兩個資料行名稱`nvarchar(50)`及位置`nvarchar(50)`，如下圖所示。 SSDT 會產生`CREATE TABLE`編寫指令碼，當您在設計工具中加入資料行。

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. 儲存**Table1.sql**檔案。

## <a name="build-and-validate-the-database"></a>建置及驗證資料庫

1. 開啟資料庫的 [專案] 功能表**TutorialDB** ，然後選取**建置**。 SSDT 會編譯您的專案中的.sql 原始程式檔，並建置資料層應用程式封裝 (dacpac) 檔案。 這可用來將資料庫發佈至您在 Linux 上的 SQL Server 執行個體。 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. 簽入組建成功訊息**輸出**Visual Studio 中的視窗。 

## <a name="publish-the-database-to-sql-server-instance-on-linux"></a>將資料庫發行至 Linux 上的 SQL Server 執行個體

1. 開啟資料庫的 [專案] 功能表**TutorialDB** ，然後選取**發佈**。

2. 按一下 **編輯**來選取您在 Linux 上的 SQL Server 執行個體。

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. 在 [連接] 對話方塊中，輸入您在 Linux、 使用者名稱和密碼的 SQL Server 執行個體的 IP 位址或主機名稱。

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. 按一下 **發佈**發佈 對話方塊上的按鈕。

5. 簽入的發行狀態**資料工具作業**視窗。

6. 按一下 **檢視結果**或是**檢視指令碼**以查看詳細資料的資料庫發行您的 SQL Server on Linux 上的結果。

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

在您順利在 Linux 上的 SQL Server 執行個體上建立新的資料庫並了解開發資料庫與原始檔控制資料庫專案的基本概念。

## <a name="next-steps"></a>後續步驟

如果您還不熟悉 T-SQL，請參閱[教學課程：撰寫 TRANSACT-SQL 陳述式]而[TRANSACT-SQL 參考 (Database Engine)]。

如需有關如何開發使用 SQL Data Tools 資料庫的詳細資訊，請參閱[SSDT MSDN 文件]

[下載並安裝 Visual Studio]: https://www.visualstudio.com/downloads/
[Download and Install SSDT]:https://aka.ms/ssdt-download
[SSDT MSDN 文件]: https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx
[教學課程：撰寫 Transact-SQL 陳述式]: https://msdn.microsoft.com/library/ms365303.aspx
[Transact-SQL 參考 (Database Engine)]: https://msdn.microsoft.com/library/bb510741.aspx
