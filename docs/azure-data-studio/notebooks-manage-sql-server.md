---
title: 管理 SQL Server 筆記本
description: 了解如何管理 Azure Data Studio 中的筆記本。 這包括開啟筆記本、進行儲存，以及變更您的巨量資料叢集連線。
author: markingmyname
ms.author: maghan
ms.reviewer: achatter, alayu, mikeray
ms.metadata: seo-lt-2019
ms.topic: conceptual
ms.prod: sql
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 03/30/2020
ms.openlocfilehash: 9b071a9d1b9e770e1443e5df539208baa4399a30
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531591"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>如何管理 Azure Data Studio 中的筆記本

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何使用 SQL Server，在 Azure Data Studio 中開啟和儲存筆記本檔案。 也會示範如何變更 SQL Server 連線。

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

## <a name="change-the-connection"></a>變更連線

若要變更筆記本的連線：

1. 選取筆記本工具列中的 [附加至]  功能表，然後選取 [變更連線]  。

   ![按一下筆記本工具列中的 [附加至] 功能表](./media/notebooks-manage-sql-server/select-attach-to-1.png)

2. 您現在可以選取最近的連線伺服器，或輸入新的連線詳細資料來連線。

   ![從 [附加至] 功能表選取伺服器](./media/notebooks-manage-sql-server/select-attach-to-2.png)

## <a name="next-steps"></a>後續步驟

如需 Azure Data Studio 中筆記本的詳細資訊，請參閱[如何在 SQL Server 2019 中使用筆記本](notebooks-guidance.md)。
