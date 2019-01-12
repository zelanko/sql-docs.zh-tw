---
title: 管理 Azure Data Studio 中的 notebook
titleSuffix: SQL Server 2019 big data clusters
description: 了解如何管理 Azure Data Studio 中的 notebook。 這包括開啟 notebook 儲存，且變更您的巨量資料叢集連線。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 107a567da4727fa5786b0b913f1c75706a23a9b7
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2019
ms.locfileid: "54241919"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>如何管理 Azure Data Studio 中的 notebook

這篇文章會示範如何開啟及儲存在 Azure 資料 Studio 中的 notebook 檔案，使用 SQL Server 2019 預覽。 它也會示範如何將您的連線變更為您 SQL Server 的巨量資料叢集。

## <a name="prerequisites"></a>先決條件

本文假設您已經有您想要使用 Azure Data Studio 中的 notebook。 如果您想要建立的 notebook，請參閱[如何在 SQL Server 2019 預覽中使用 notebook](notebooks-guidance.md)。 若要使用 Azure Data Studio notebook，您必須符合下列必要條件：

- [部署巨量資料叢集](quickstart-big-data-cluster-deploy.md)。
- [SQL Server 2019 巨量資料工具](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **kubectl**

## <a name="open-a-notebook"></a>開啟 notebook

有數種方式來開啟**開啟 Notebook**對話方塊。 您可以使用 [檔案] 功能表、 儀表板和命令選擇區。 下列各節描述每個方法。

### <a name="file-menu"></a>[檔案] 功能表

選取 **開啟舊檔**從 檔案 功能表 Ctrl + O (Windows) 和 Cmd + O (Mac)。

![開啟 開啟檔案 對話方塊，選取 開啟舊檔](./media/notebooks-how-to-manage/open-file-1.png) 

### <a name="dashboard"></a>儀表板

按一下 **開啟 Notebook**儀表板以開啟 檔案開啟的對話方塊。

![開啟儀表板中選取 開啟 Notebook 的 開啟檔案 對話方塊](./media/notebooks-how-to-manage/open-file-2.png) 

### <a name="command-palette"></a>命令選擇區

使用命令**檔案：開啟**從命令選擇區輸入 Ctrl + Shift + P （在 Windows) 和 Cmd + Shift + P （在 Mac)。

![在命令選擇區輸入 File:Open 開啟 [開啟檔案] 對話方塊](./media/notebooks-how-to-manage/open-file-3.png)

## <a name="save-a-notebook"></a>儲存 notebook

目前沒有儲存 notebook 的一種方法。 您必須選取**儲存**從 notebook 工具列。

![儲存 notebook 工具列中按一下 儲存的檔案](./media/notebooks-how-to-manage/save-file-1.png)

> [!NOTE]
> 下列方法目前不要儲存變更至 notebook:
>
> - **檔案儲存**，**存新檔...** 並**儲存所有檔案**從 [檔案] 功能表的命令。
> - **檔案：儲存**在命令選擇區輸入命令。

## <a name="change-the-big-data-cluster"></a>變更巨量資料叢集

若要變更 SQL Server 的巨量資料叢集，notebook:

1. 按一下 **附加至**從 notebook 工具列的功能表。

   ![按一下 附加至 notebook 工具列中的功能表](./media/notebooks-how-to-manage/select-attach-to-1.png)

2. 按一下 從伺服器**附加至**功能表。

   ![功能表，然後從 附加中選取伺服器](./media/notebooks-how-to-manage/select-attach-to-2.png)

## <a name="next-steps"></a>後續步驟

如需 Azure Data Studio 中的 notebook 的詳細資訊，請參閱[如何在 SQL Server 2019 預覽中使用 notebook](notebooks-guidance.md)。