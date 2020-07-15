---
title: SQL Database Projects 延伸模組
description: 安裝和使用適用於 Azure Data Studio 的 SQL Database Projects 延伸模組 (預覽)
ms.custom: seodec18
ms.date: 06/25/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 609af04cec2f6eaaaf1890e19c6d85fbd4bd5b8a
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/29/2020
ms.locfileid: "85519147"
---
# <a name="sql-database-projects-extension-preview"></a>SQL Database Projects 延伸模組 (預覽)

SQL Database Projects 延伸模組 (預覽) 適用於在以專案為基礎的開發環境中開發 SQL 資料庫。 此延伸模組目前處於預覽狀態，可在 [Azure Data Studio 測試人員組建](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main)中使用。


## <a name="install-the-sql-database-projects-extension"></a>安裝 SQL Database Projects 延伸模組

1. 若要開啟延伸模組管理員並存取可用的延伸模組，請選取延伸模組圖示，或選取 [檢視] 功能表中的 [延伸模組]。
2. 在延伸模組搜尋方塊中鍵入延伸模組的全名或部分名稱，並找出 *SQL Database Projects* 延伸模組。 選取可用的延伸模組，檢視詳細資料。

   ![安裝擴充功能](media/extensions/sql-database-projects-extension/install-database-projects.png)

3. 選取您想要的延伸模組並加以**安裝**。
4. 選取 [重新載入]，啟用此延伸模組 (只有當您第一次安裝延伸模組時才需要)。
5. 從活動列選取檔案圖示，或從 [檢視] 功能表中選取 [總管]。 [Projects] \(專案\) 的新 Viewlet 隨即可供使用。

   > [!NOTE]
   > 建議搭配 SQL Database Projects 延伸模組一同安裝 [Schema Compare 延伸模組](schema-compare-extension.md)，以取得完整功能。

## <a name="getting-started-with-database-projects"></a>開始使用資料庫專案

* 前往位於 [總管] 下方的 [Projects] \(專案\) Viewlet，或在命令選擇區中搜尋 **New Database Project** (新增資料庫專案)，以建立新的資料庫專案。
* 您可透過在命令選擇區中的 [Open Database Project] \(開啟資料庫專案\) 來開啟現有資料庫專案。
* 使用命令選擇區中的 [Import New Database Project] \(匯入新的資料庫專案\) 來從現有資料庫專案開始。

   ![新增 Viewlet](media/extensions/sql-database-projects-extension/projects-viewlet.png)


### <a name="create-an-empty-database-project"></a>建立空白資料庫專案

 在位於 [總管] 下方的 [Projects] \(專案\) Viewlet 中，按一下 [New Project] \(新增專案\) 按鈕，然後在出現的文字輸入中輸入專案名稱。  在出現的 [選取資料夾] 對話方塊中，選取專案資料夾的目錄、.sqlproj 檔，以及要存放在其中的其他內容。
空白專案隨即開啟，並顯示在 [Projects] \(專案\) Viewlet 中以供編輯。

### <a name="open-an-existing-project"></a>開啟現有專案

在 [Projects] \(專案\) Viewlet 中，按一下 [Open Project] \(開啟專案\) 按鈕，然後從出現的檔案選擇器中開啟現有 *.sqlproj* 檔案。 現有的專案可來自 Azure Data Studio 或 [Visual Studio SQL Server Data Tools](../ssdt/sql-server-data-tools.md)。

現有專案隨即開啟，且其內容會顯示在 [Projects] \(專案\) Viewlet 中以供編輯。

### <a name="create-a-database-project-from-an-existing-database"></a>從現有資料庫建立資料庫專案

在 [Projects] \(專案\) Viewlet 中，按一下 [Import Project from Database] \(從資料庫匯入專案\) 按鈕並連線到 SQL Server。  建立連線後，從可用的資料庫清單選取資料庫，並設定專案的名稱。

最後，選取擷取的目標結構。  新專案隨即開啟，且包含所選取資料庫內容的 SQL 指令碼。

## <a name="build-and-publish"></a>建置和發佈

部署資料庫專案的方式是在 Azure Data Studio 的 SQL Database Projects 延伸模組中將專案建置成[資料層應用程式檔案](../relational-databases/data-tier-applications/data-tier-applications.md) (DACPAC)，並發佈到支援的平台。 如需此程序的詳細資訊，請參閱[建置和發佈專案](sql-database-project-extension-build.md)。

## <a name="schema-compare"></a>結構描述比較
如果有安裝 Schema Compare 延伸模組，則 SQL Database Projects 延伸模組會和 [Schema Compare 延伸模組](schema-compare-extension.md)互動，將專案的內容與 dacpac 或現有資料庫比較。  產生的結構描述比較可用來檢視和將差異從來源套用到目標。

## <a name="next-steps"></a>後續步驟

- [使用 Azure Data Studio 的 SQL Database Projects 延伸模組建置和發佈專案](sql-database-project-extension-build.md)
- [資料層應用程式](../relational-databases/data-tier-applications/data-tier-applications.md)