---
title: 管理：Azure Data Studio 筆記本
titleSuffix: SQL Server Big Data Clusters
description: 使用來自 Azure Data Studio 的筆記本，來管理巨量資料叢集與進行疑難排解。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d2a051e297b48ed8d813fce0e0e8ffa748a84d16
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75252017"
---
# <a name="manage-sql-server-big-data-clusters-with-azure-data-studio-notebooks"></a>使用 Azure Data Studio 筆記本管理 SQL Server 巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 提供包含筆記本的 Azure Data Studio 延伸模組。 筆記本提供了文件和程式碼，可供您用來在 Azure Data Studio 中管理 SQL Server 2019 巨量資料叢集。

[筆記本](notebooks-guidance.md)原本是實作為開放原始碼專案，而現已合併至 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download) \(部分機器翻譯\)。 您現在可以將 Markdown 用於文字儲存格中的文字，也可以使用其中一個可用的核心，在程式碼儲存格中撰寫程式碼。

您可以使用筆記本來部署 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的巨量資料叢集。

除了筆記本之外，您也可以看到一組筆記本集合，也就是所謂的 Jupyter Book。 Jupyter Book 提供目錄，以協助您瀏覽筆記本集合，讓您可以輕鬆地找到所需的筆記本，不論是要針對 SQL Server 進行疑難排解或是要檢視叢集狀態。

## <a name="prerequisites"></a>Prerequisites

您需要下列必要元件才能開啟筆記本：

* 最新版的 [Azure Data Studio Insiders 組建](https://aka.ms/azuredatastudio-rc) \(英文\)
* 在 Azure Data Studio 中安裝 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 延伸模組

除了以上必要元件之外，若要部署 SQL Server 2019 巨量資料叢集叢集，您也需要：

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="access-troubleshooting-notebooks"></a>存取疑難排解筆記本
有三種方式可存取疑難排解筆記本。

### <a name="command-palette"></a>命令選擇區
1. 選取 [檢視]   > [命令調色盤]  。
2. 輸入 **Jupyter Book：SQL Server 2019 指南**。

內含包含 SQL Server 巨量資料叢集相關疑難排解筆記本之 Jupyter Book 的 Jupyter Book viewlet 將會開啟。

### <a name="sql-master-dashboard"></a>SQL 主要儀表板
1. 在您安裝 Azure Data Studio Insiders 之後，請連線至 SQL Server 巨量資料叢集執行個體。
2. 連接到執行個體之後，以滑鼠右鍵按一下 [連線]  底下的伺服器名稱，然後選取 [管理]  。
3. 在儀表板中，選取 [SQL Server 巨量資料叢集]  。 選取 [SQL Server 2019 指南]  ，以開啟包含您所需筆記本的 Jupyter Book。
    ![儀表板中的 Jupyter 筆記本](media/manage-notebooks/jupyter-book-button.png)

1. 按一下筆記本以尋找您需要完成的工作。

### <a name="controller-dashboard"></a>控制器儀表板
1. 在 [連線]  檢視中，展開 [SQL Server 巨量資料叢集]  。
2. 新增控制器端點詳細資料。
3. 連線到控制器之後，以滑鼠右鍵按一下端點，然後選取 [管理]  。
4. 載入儀表板之後，選取 [疑難排解]  開啟 Jupyter Book 疑難排解指南。

## <a name="use-troubleshooting-notebooks"></a>使用疑難排解筆記本
1. 在 Jupyter Book 目錄中尋找所需的疑難排解指南。
1. 筆記本已優化，因此您只需要選取 [執行資料格]  。 此動作將會個別執行筆記本中的每個資料格，直到筆記本完成為止。
1. 如果發現錯誤，Jupyter Book 將會建議您可以執行以修正錯誤的筆記本。 請遵循建議的步驟，然後再次執行筆記本。

## <a name="next-steps"></a>後續步驟
如需 Azure Data Studio 中筆記本的詳細資訊，請參閱[如何在 SQL Server 中使用筆記本](notebooks-guidance.md)。
