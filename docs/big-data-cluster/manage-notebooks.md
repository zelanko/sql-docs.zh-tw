---
title: 使用 Azure Data Studio 筆記本管理 SQL Server 巨量資料叢集
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: 使用來自 Azure Data Studio 的筆記本，來管理巨量資料叢集與進行疑難排解。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1a6156dad127ea2a86e8a6f4dfbdd6f692fd8f6e
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893655"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>使用 Azure Data Studio 筆記本管理 SQL Server 的巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 提供包含筆記本的 Azure Data Studio 延伸模組。 筆記本所包含的文件和程式碼，可供您用來在 Azure Data Studio 中管理 SQL Server 的巨量資料叢集。

[筆記本](notebooks-guidance.md)原本是實作為開放原始碼專案，而現已實作至 [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download) \(部分機器翻譯\)。 您現在可以將 Markdown 用於文字儲存格中的文字，也可以使用其中一個可用的核心，在程式碼儲存格中撰寫程式碼。

您可以使用筆記本來部署 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的巨量資料叢集。

除了筆記本以外, 使用者也可以查看筆記本的集合, 稱為 Jupyter 書籍。 Jupyter Book 提供瀏覽筆記本集合的目錄，讓使用者可以輕鬆地找到所需的筆記本，不論是針對 SQL Server 進行疑難排解或檢視叢集狀態。

## <a name="prerequisites"></a>先決條件

必須滿足下列先決條件才能啟動筆記本：

* 最新版的 [Azure Data Studio Insiders 組建](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master) \(英文\)
* 在 Azure Data Studio 中安裝 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 延伸模組

除了上述，部署 SQL Server 2019 巨量資料叢集也需要：

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="accessing-troubleshooting-notebooks"></a>存取疑難排解筆記本

1. 安裝 Azure Data Studio Insiders 之後，請連線至 SQL Server 巨量資料叢集執行個體。
2. 成功連線之後，請在 [連線] viewlet 中，以滑鼠右鍵按一下您的伺服器名稱，然後按一下 [管理]。
3. 在儀表板上，按一下 [SQL Server 巨量資料叢集]。 按一下 [SQL Server 2019 指南]，以使用您所需的筆記本開啟 Jupyter Book。
    ![按鈕](media/manage-notebooks/jupyter-book-button.png)

1. 在 [資料夾選擇器] 視窗中，選擇要儲存 Jupyter Book 的位置。
2. 按一下 [重新載入] 來重新載入 Azure Data Studio，以查看您的 Jupyter Book。 按一下[開啟新的執行個體]，以使用 Jupyter Book 開啟新的 Azure Data Studio 執行個體。
3. 在 [Explorer] 檢視中，您應該會看到稱為 **Books** 的區段。 如果未展開，請按一下它來查看筆記本。
4. 按一下筆記本以尋找您需要完成的工作。

## <a name="next-steps"></a>後續步驟
如需 Azure Data Studio 中筆記本的詳細資訊，請參閱[如何在 SQL Server 2019 預覽中使用筆記本](notebooks-guidance.md)。
