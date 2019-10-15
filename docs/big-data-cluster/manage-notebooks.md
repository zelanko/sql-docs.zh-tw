---
title: 使用 Azure Data Studio 筆記本管理 SQL Server Big Data 叢集
titleSuffix: Manage SQL Server Big Data Clusters with Azure Data Studio notebooks
description: 使用來自 Azure Data Studio 的筆記本，來管理巨量資料叢集與進行疑難排解。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e22b16cf8658e53e6bdc5db0fcd82692f3730fc7
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313674"
---
# <a name="manage-sql-server-big-data-clusters-with-azure-data-studio-notebooks"></a>使用 Azure Data Studio 筆記本管理 SQL Server Big Data 叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 提供包含筆記本的 Azure Data Studio 延伸模組。 筆記本提供的檔和程式碼可讓您在 Azure Data Studio 中用來管理 SQL Server 2019 Big Data 叢集。

[筆記本](notebooks-guidance.md)原本實作為開放原始碼專案，已併入[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download)。 您現在可以將 Markdown 用於文字儲存格中的文字，也可以使用其中一個可用的核心，在程式碼儲存格中撰寫程式碼。

您可以使用筆記本來部署 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的巨量資料叢集。

除了筆記本以外，您還可以查看筆記本的集合，稱為 Jupyter 書籍。 Jupyter 書籍提供的目錄可協助您流覽筆記本集合，讓您可以輕鬆地找到所需的筆記本，不論您是要針對 SQL Server 或查看叢集狀態進行疑難排解。

## <a name="prerequisites"></a>必要條件

若要開啟筆記本，您需要下列必要條件：

* 最新版的[Azure Data Studio 內部人員組建](https://aka.ms/azuredatastudio-rc)
* @No__t-0 延伸模組，安裝在 Azure Data Studio

除了這些必要條件之外，若要部署 SQL Server 2019 Big Data 叢集，您也需要：

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="access-troubleshooting-notebooks"></a>存取筆記本疑難排解
有三種方式可存取疑難排解筆記本。

### <a name="command-palette"></a>命令選擇區
1. 選取 [ **View** > ]**命令**選擇區。
2. 輸入 @no__t 0Jupyter 書籍：SQL Server 2019 指南 @ no__t-0。

與 Jupyter 書籍 viewlet 的 Jupyter 書籍，其中包含與 SQL Server Big Data 叢集相關的疑難排解筆記本將會開啟。

### <a name="sql-master-dashboard"></a>SQL 主儀表板
1. 在您安裝 Azure Data Studio 內部人員之後，請連接到 SQL Server Big Data 叢集實例。
2. 連接到實例之後，以滑鼠右鍵按一下 [**連接**] 底下的伺服器名稱，然後選取 [**管理**]。
3. 在儀表板中，選取 [ **SQL Server Big Data Cluster**]。 選取**SQL Server 2019 指南**，開啟包含所需筆記本的 Jupyter 書籍。
    在儀表板中 @no__t 0Jupyter 筆記本 @ no__t-1

1. 選取您需要完成之工作的筆記本。

### <a name="controller-dashboard"></a>控制器儀表板
1. 在 [**連接**] 視圖中，展開 [ **SQL Server Big Data**叢集]。
2. 新增控制器端點詳細資料。
3. 連線到控制器之後，以滑鼠右鍵按一下端點，然後選取 [**管理**]。
4. 在儀表板載入之後，選取 [**疑難排解**] 以開啟 Jupyter 書籍疑難排解指南。

## <a name="use-troubleshooting-notebooks"></a>使用疑難排解筆記本
1. 在您的 Jupyter 書籍目錄中，尋找您需要的疑難排解指南。
1. 筆記本已優化，因此您只需要選取 [**執行儲存格**]。 此動作會個別執行筆記本中的每個資料格，直到筆記本完成為止。
1. 如果發現錯誤，Jupyter 書將會建議您可以執行以修正錯誤的筆記本。 遵循建議的步驟，然後再次執行筆記本。

## <a name="next-steps"></a>後續步驟
如需 Azure Data Studio 中筆記本的詳細資訊，請參閱[如何在 SQL Server 2019 Preview 中使用筆記本](notebooks-guidance.md)。
