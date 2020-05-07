---
title: 如何管理筆記本
description: 了解如何管理 Azure Data Studio 中的筆記本。 這包括開啟筆記本、進行儲存，以及變更 SQL 連線或 Python 核心。
author: markingmyname
ms.author: maghan
ms.reviewer: achatter, alayu, mikeray
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: 435290bd45e79c835ba134bb732f1672dc31c2cf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "82178695"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>如何管理 Azure Data Studio 中的筆記本

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何在 Azure Data Studio 中開啟和儲存筆記本檔案。 同時也示範如何變更 SQL Server 連線或 Python 核心。

## <a name="open-a-notebook"></a>開啟筆記本

您可以利用多種方式開啟 [開啟筆記本]  對話方塊。 您可以使用 [檔案] 功能表、儀表板和命令選擇區。 下列各節將描述各種方法。

### <a name="file-menu"></a>[檔案] 功能表

從 [檔案] 功能表選取 [開啟檔案]  (Ctrl+O (Windows) 和 Cmd+O (Mac))。

![選取 [開啟檔案]，開啟 [開啟檔案] 對話方塊](./media/notebooks-manage-sql-server/open-file-1.png)

### <a name="dashboard"></a>儀表板

在儀表板中按一下 [開啟筆記本]  ，開啟 [開啟檔案] 對話方塊。

![在儀表板中選取 [開啟筆記本]，開啟 [開啟檔案] 對話方塊](./media/notebooks-manage-sql-server/open-file-2.png) 

### <a name="command-palette"></a>命令選擇區

從命令選擇區使用命令 **File:Open** (透過在 Windows 鍵入Ctrl+Shift+P 或在 Mac 鍵入 Cmd+Shift+P)。

![輸入檔案以開啟 [開啟檔案] 對話方塊：在命令選擇區中開啟](./media/notebooks-manage-sql-server/open-file-3.png)

## <a name="save-a-notebook"></a>儲存筆記本

目前只能利用一種方式來儲存筆記本。 選取筆記本工具列中的 [儲存]  。

![選取筆記本工具列中的 [儲存] 以儲存檔案](./media/notebooks-manage-sql-server/save-file-1.png)

> [!NOTE]
> 下列方法目前無法儲存筆記本的變更：
>
> - 從 [檔案] 功能表的 [儲存檔案]  、[另存新檔...]  和 [儲存所有檔案]  命令。
> - 在命令選擇區中輸入 **File:Save** 命令。

## <a name="change-the-sql-connection"></a>變更 SQL 連線

若要變更筆記本的 SQL 連線：

1. 選取筆記本工具列中的 [附加至]  功能表，然後選取 [變更連線]  。

   ![按一下筆記本工具列中的 [附加至] 功能表](./media/notebooks-manage-sql-server/select-attach-to-1.png)

2. 您現在可以選取最近的連線伺服器，或輸入新的連線詳細資料來連線。

   ![從 [附加至] 功能表選取伺服器](./media/notebooks-manage-sql-server/select-attach-to-2.png)

## <a name="change-the-python-kernel"></a>變更 Python 核心

第一次開啟 Azure Data Studio 時，隨即會顯示 [為筆記本設定 Python]  頁面。 您可選取下列其中一項：

- [新增 Python 安裝]  ，以安裝適用於 Azure Data Studio 的新 Python 複本，或
- [使用現有的 Python 安裝]  ，以指定現有 Python 安裝的路徑來供 Azure Data Studio 使用

若要查看使用中 Python 核心的位置和版本，請建立程式碼資料格，並執行下列 Python 命令：

```python
import os
import sys
print(sys.version_info)
print(os.path.dirname(sys.executable))
```

變更為不同的 Python 安裝：

1. 從 [檔案]  功能表選取 [喜好設定]  ，然後選取 [設定]  。
1. 捲動至 [延伸模組]  底下的 [筆記本組態]  。
1. 在 [使用現有的 Python]  底下，取消核取 [筆記本所使用現有 Python安裝的本機路徑] 選項。
1. 重新啟動 Azure Data Studio。

當顯示 [Configure Python for Notebooks] \(為筆記本設定 Python\)  頁面時，您可選擇建立新的 Python 安裝，或指定現有安裝的路徑。

## <a name="next-steps"></a>後續步驟

如需 Azure Data Studio 中 SQL 筆記本的詳細資訊，請參閱[如何在 SQL Server 2019 中使用筆記本](notebooks-guidance.md)。
