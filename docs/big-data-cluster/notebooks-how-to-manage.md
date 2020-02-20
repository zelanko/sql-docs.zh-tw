---
title: 管理筆記本：Azure Data Studio
titleSuffix: SQL Server Big Data Clusters
description: 了解如何管理 Azure Data Studio 中的筆記本。 這包括開啟筆記本、進行儲存，以及變更您的巨量資料叢集連線。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8cf37ff6a4ad5e2b627fa5d968391cc5a7597a4a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244093"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>如何管理 Azure Data Studio 中的筆記本

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何使用 SQL Server，在 Azure Data Studio 中開啟和儲存筆記本檔案。 它也示範如何變更您的 SQL Server 巨量資料叢集連線。

## <a name="prerequisites"></a>Prerequisites

本文假設您已擁有要在 Azure Data Studio 中使用的筆記本。 如果您想要建立筆記本，請參閱[如何在 SQL Server 中使用筆記本](notebooks-guidance.md)。 若要在 Azure Data Studio 中使用筆記本，您必須符合下列必要條件：

- [部署巨量資料叢集](quickstart-big-data-cluster-deploy.md)。
- [SQL Server 2019 巨量資料工具](deploy-big-data-tools.md)：
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **kubectl**

## <a name="open-a-notebook"></a>開啟筆記本

您可以利用多種方式開啟 [開啟筆記本]  對話方塊。 您可以使用 [檔案] 功能表、儀表板和命令選擇區。 下列各節將描述各種方法。

### <a name="file-menu"></a>[檔案] 功能表

從 [檔案] 功能表選取 [開啟檔案]  (Ctrl+O (Windows) 和 Cmd+O (Mac))。

![選取 [開啟檔案]，開啟 [開啟檔案] 對話方塊](./media/notebooks-how-to-manage/open-file-1.png) 

### <a name="dashboard"></a>儀表板

在儀表板中按一下 [開啟筆記本]  ，開啟 [開啟檔案] 對話方塊。

![在儀表板中選取 [開啟筆記本]，開啟 [開啟檔案] 對話方塊](./media/notebooks-how-to-manage/open-file-2.png) 

### <a name="command-palette"></a>命令選擇區

從命令選擇區使用命令 **File:Open** (透過在 Windows 鍵入Ctrl+Shift+P 或在 Mac 鍵入 Cmd+Shift+P)。

![在命令選擇區中輸入 File:Open，開啟 [開啟檔案] 對話方塊](./media/notebooks-how-to-manage/open-file-3.png)

## <a name="save-a-notebook"></a>儲存筆記本

目前只能利用一種方式儲存筆記本。 您必須選取筆記本工具列中的 [儲存]  。

![按一下筆記本工具列中的 [儲存]，儲存檔案](./media/notebooks-how-to-manage/save-file-1.png)

> [!NOTE]
> 下列方法目前無法儲存筆記本的變更：
>
> - 從 [檔案] 功能表的 [儲存檔案]  、[另存新檔...]  和 [儲存所有檔案]  命令。
> - 在命令選擇區中輸入 **File:Save** 命令。

## <a name="change-the-big-data-cluster"></a>變更巨量資料叢集

若要變更筆記本的 SQL Server 巨量資料叢集：

1. 按一下筆記本工具列中的 [附加至]  功能表。

   ![按一下筆記本工具列中的 [附加至] 功能表](./media/notebooks-how-to-manage/select-attach-to-1.png)

2. 在 [附加至]  功能表中，按一下伺服器。

   ![從 [附加至] 功能表選取伺服器](./media/notebooks-how-to-manage/select-attach-to-2.png)

## <a name="next-steps"></a>後續步驟

如需 Azure Data Studio 中筆記本的詳細資訊，請參閱[如何在 SQL Server 2019 中使用筆記本](notebooks-guidance.md)。
