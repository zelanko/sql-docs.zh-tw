---
title: SQL Database Projects 延伸模組
description: 安裝和使用適用於 Azure Data Studio 的 SQL Database Projects 延伸模組。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: ''
ms.date: 10/22/2020
ms.openlocfilehash: e4030cac39eca0d57af3bf2bcefad293e83971c2
ms.sourcegitcommit: a2182276ba00c48dc1475b9c7dfa45179d4416dc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2020
ms.locfileid: "94704163"
---
# <a name="sql-database-projects-extension-preview"></a>SQL Database Projects 延伸模組 (預覽)

SQL Database Projects 延伸模組 (預覽) 適用於在以專案為基礎的開發環境中開發 SQL 資料庫。 


## <a name="features"></a>特性

1. 從連線的資料庫建立專案。
2. 建立新的空白專案。
3. 開啟先前在 [Azure Data Studio](sql-database-project-extension-getting-started.md) 或 [SQL Server Data Tools](../../ssdt/sql-server-data-tools.md) 中建立的專案。
4. 編輯專案，可在專案中新增或移除資料表、檢視、預存程序或自訂指令碼。
5. 整理資料夾中的檔案/指令碼。
6. 新增對系統資料庫或使用者 dacpac 的參考。
7. 組建單一專案。
8. 部署單一專案。
9. 從部署設定檔載入連線詳細資料 (SQL Windows 驗證) 與 SQLCMD 變數。

觀看這段簡短的 10 分鐘影片，以取得 Azure Data Studio 中 SQL Database 專案延伸模組的簡介：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Build-SQL-Database-Projects-Easily-in-Azure-Data-Studio/player?WT.mc_id=dataexposed-c9-niner]

## <a name="install-the-sql-database-projects-extension"></a>安裝 SQL Database Projects 延伸模組

1. 開啟延伸模組管理員以存取可用的延伸模組。  若要這樣做，請選取延伸模組圖示，或在 [檢視] 功能表中選取 [延伸模組]。
2. 在延伸模組搜尋方塊中鍵入延伸模組的全名或部分名稱，並找出 *SQL Database Projects* 延伸模組。 選取可用的延伸模組，檢視詳細資料。

   ![安裝擴充功能](media/sql-database-projects-extension/install-database-projects.png)

3. 選取您想要的延伸模組並加以 **安裝**。
4. 選取 [重新載入]，啟用此延伸模組 (只有當您第一次安裝延伸模組時才需要)。
5. 從活動列選取檔案圖示，或從 [檢視] 功能表中選取 [總管]。 [Projects] \(專案\) 的新 Viewlet 隨即可供使用。

   > [!NOTE]
   > 專案建置功能需要 .NET Core SDK，如果延伸模組無法偵測到 .NET Core SDK，即會提示您進行安裝。  .NET Core SDK (3.1 或更新版本) 可以從 [https://dotnet.microsoft.com/download/dotnet-core/3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1) 下載並安裝。

   > [!NOTE]
   > 建議搭配 SQL Database Projects 延伸模組一同安裝 [Schema Compare 延伸模組](schema-compare-extension.md)，以取得完整功能。

## <a name="known-limitations"></a>已知限制

- Azure Data Studio Viewlet 中目前不支援將檔案載入為連結，不過，檔案將會載入到樹狀結構的最上層，而組建將如預期般納入這些檔案。
- 在 DacFx 的 .NET Core 版本中，不支援專案中的 SQLCLR 物件。
- 工作 (組建/發佈) 並非使用者定義。
- 發佈 DacFx 所定義的目標。
- WSL 環境支援有限。

## <a name="next-steps"></a>接下來的步驟

- [開始使用 SQL 資料庫專案延伸模組](sql-database-project-extension-getting-started.md)
- [使用 Azure Data Studio 的 SQL Database Projects 延伸模組建置和發佈專案](sql-database-project-extension-build.md)
