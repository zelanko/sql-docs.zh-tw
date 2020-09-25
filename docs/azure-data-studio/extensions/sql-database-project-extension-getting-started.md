---
title: 開始使用 SQL Database Projects 延伸模組
description: 開始使用適用於 Azure Data Studio 的 SQL Database Projects 延伸模組
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: ''
ms.date: 07/30/2020
ms.openlocfilehash: cd818010b068ccd206f411ce8c578386d0b8772f
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123176"
---
# <a name="getting-started-with-the-sql-database-projects-extension-preview"></a>開始使用 SQL Database Projects 延伸模組 (預覽)

此文章描述開始使用 SQL 資料庫專案延伸模組的三種方式：

1. 前往位於 [總管] 下方的 [Projects] \(專案\) Viewlet，或在命令選擇區中搜尋 **New Database Project** (新增資料庫專案)，以建立新的資料庫專案。
2. 您可透過在命令選擇區中的 [Open Database Project] \(開啟資料庫專案\) 來開啟現有資料庫專案。
3. 使用命令選擇區中的 [Import New Database Project] \(匯入新的資料庫專案\) 來從現有資料庫專案開始。

    ![新增 Viewlet](media/sql-database-projects-extension/projects-viewlet.png)

## <a name="create-an-empty-database-project"></a>建立空白資料庫專案

在 [總管] 下方的 [專案] Viewlet 中，選取 [新增專案] 按鈕，然後在出現的文字輸入內容中輸入專案名稱。  在出現的 [選取資料夾] 對話方塊中，選取專案資料夾的目錄、.sqlproj 檔，以及要存放在其中的其他內容。
空白專案隨即開啟，並顯示在 [Projects] \(專案\) Viewlet 中以供編輯。

## <a name="open-an-existing-project"></a>開啟現有的專案

在 [專案] Viewlet 中，選取 [開啟專案] 按鈕，然後從出現的檔案選擇器中開啟現有的 .sqlproj 檔案。 現有的專案可來自 Azure Data Studio 或 [Visual Studio SQL Server Data Tools](../../ssdt/sql-server-data-tools.md)。

現有專案隨即開啟，且其內容會顯示在 [Projects] \(專案\) Viewlet 中以供編輯。

## <a name="create-a-database-project-from-an-existing-database"></a>從現有資料庫建立資料庫專案

在 [專案] Viewlet 中，選取 [從資料庫匯入專案] 按鈕並連線到 SQL Server。  建立連線後，從可用的資料庫清單選取資料庫，並設定專案的名稱。

最後，選取擷取的目標結構。  新專案隨即開啟，且包含所選取資料庫內容的 SQL 指令碼。

## <a name="build-and-publish"></a>建置和發佈

部署資料庫專案的方式是在 Azure Data Studio 的 SQL Database Projects 延伸模組中將專案建置成[資料層應用程式檔案](../../relational-databases/data-tier-applications/data-tier-applications.md) (DACPAC)，並發佈到支援的平台。 如需此程序的詳細資訊，請參閱[建置和發佈專案](sql-database-project-extension-build.md)。

## <a name="schema-compare"></a>結構描述比較

如果有安裝 Schema Compare 延伸模組，則 SQL Database Projects 延伸模組會和 [Schema Compare 延伸模組](schema-compare-extension.md)互動，將專案的內容與 dacpac 或現有資料庫比較。  產生的結構描述比較可用來檢視和將差異從來源套用到目標。

## <a name="next-steps"></a>後續步驟

- [使用 Azure Data Studio 的 SQL Database Projects 延伸模組建置和發佈專案](sql-database-project-extension-build.md)