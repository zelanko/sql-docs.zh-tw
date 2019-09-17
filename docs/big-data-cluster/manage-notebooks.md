---
title: 使用 Azure Data Studio 筆記本管理 SQL Server 巨量資料叢集
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: 使用來自 Azure Data Studio 的筆記本，來管理巨量資料叢集與進行疑難排解。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 09/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cb2fcaf7431b5d79698af009b533ee49254777fe
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846655"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>使用 Azure Data Studio 筆記本管理 SQL Server 的巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 提供包含筆記本的 Azure Data Studio 延伸模組。 筆記本所包含的文件和程式碼，可供您用來在 Azure Data Studio 中管理 SQL Server 的巨量資料叢集。

[筆記本](notebooks-guidance.md)原本是實作為開放原始碼專案，而現已實作至 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download) \(部分機器翻譯\)。 您現在可以將 Markdown 用於文字儲存格中的文字，也可以使用其中一個可用的核心，在程式碼儲存格中撰寫程式碼。

您可以使用筆記本來部署 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的巨量資料叢集。

除了筆記本以外，使用者也可以查看筆記本的集合，稱為 Jupyter 書籍。 Jupyter Book 提供瀏覽筆記本集合的目錄，讓使用者可以輕鬆地找到所需的筆記本，不論是針對 SQL Server 進行疑難排解或檢視叢集狀態。

## <a name="prerequisites"></a>必要條件

必須滿足下列先決條件才能啟動筆記本：

* 最新版的 [Azure Data Studio Insiders 組建](https://aka.ms/azuredatastudio-rc) \(英文\)
* 在 Azure Data Studio 中安裝 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 延伸模組

除了上述，部署 SQL Server 2019 巨量資料叢集也需要：

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="accessing-troubleshooting-notebooks"></a>存取疑難排解筆記本
有三種方式可存取疑難排解筆記本。

### <a name="command-palette"></a>命令選擇區
1. 按一下 [**流覽**] 和 [**命令**選擇區]
2. 輸入「Jupyter 書籍：SQL Server 2019 指南」
3. 這會開啟 Jupyter 書籍 Viewlet，其中包含 Jupyter 書籍，內含與 SQL Server Big Data 叢集相關的 TSG。

### <a name="sql-master-dashboard"></a>SQL 主儀表板
1. 安裝 Azure Data Studio Insiders 之後，請連線至 SQL Server 巨量資料叢集執行個體。
2. 成功連線之後，請在 [連線] viewlet 中，以滑鼠右鍵按一下您的伺服器名稱，然後按一下 [管理]。
3. 在儀表板上，按一下 [SQL Server 巨量資料叢集]。 按一下 [SQL Server 2019 指南]，以使用您所需的筆記本開啟 Jupyter Book。
    ![按鈕](media/manage-notebooks/jupyter-book-button.png)

1. 這會開啟已開啟 TSG Jupyter 書籍的 Jupyter 書籍 viewlet。
4. 按一下筆記本以尋找您需要完成的工作。

### <a name="controller-dashboard"></a>控制器儀表板
1. 在 [**連接**] 視圖中，展開 [ **SQL Server Big Data**叢集]。
2. 新增控制器端點詳細資料。
3. 成功連接到控制器之後，以滑鼠右鍵按一下端點，然後按一下 [**管理]。**
4. 在儀表板載入之後，按一下 [疑難排解] 以啟動 Jupyter Book TSG。

## <a name="how-to-use-troubleshooting-notebooks"></a>如何使用筆記本疑難排解
1. 查看現有的 Jupyter 書籍目錄，直到您找到所需的 TSG。
1. 所有筆記本都已優化，使用者只需要按一下 [**執行儲存格]。** 這會個別執行筆記本中的每個資料格，直到完成為止。
1. 如果您遇到錯誤，Jupyter 書將會建議您可以執行以修正錯誤的筆記本。 依照步驟執行，然後重新執行筆記本。

## <a name="next-steps"></a>後續步驟
如需 Azure Data Studio 中筆記本的詳細資訊，請參閱[如何在 SQL Server 2019 預覽中使用筆記本](notebooks-guidance.md)。
