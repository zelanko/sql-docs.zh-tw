---
title: 使用控制器儀表板管理 SQL Server big data cluster
titleSuffix: Manage SQL Server big data cluster with controller dashboard
description: 使用來自 Azure Data Studio 的筆記本，來管理巨量資料叢集與進行疑難排解。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 08/29/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5fadb9b069e6f70cb780e6dc69295f63330a683a
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160724"
---
# <a name="manage-big-data-clusters-for-sql-server-controller-dashboard"></a>管理 SQL Server 控制器儀表板的海量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

除了**azdata**和叢集狀態筆記本以外, 還有另一種方式可以查看 SQL Server Big Data 叢集的狀態。 您現在可以透過 [連線] viewlet 來新增 SQL Server Big Data Cluster 控制器。 這可讓您使用儀表板來查看叢集健全狀況。

![儀表板](media/manage-with-controller-dashboard/controller-dashboard.png)
## <a name="prerequisites"></a>必要條件

啟動筆記本需要下列必要條件:

* 最新版的 [Azure Data Studio Insiders 組建](https://docs.microsoft.com/sql/big-data-cluster/deploy-big-data-tools?view=sqlallproducts-download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc) \(英文\)
* 在 Azure Data Studio 中安裝 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 延伸模組

除了以上以外, SQL Server 2019 Big Data 叢集也需要:

* **azdata**
    - [Linux 套件管理員](deploy-install-azdata-linux-package.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)


## <a name="add-sql-server-big-data-cluster-controller"></a>新增 SQL Server big data 叢集控制器

1. 在左窗格中, 按一下 [連接] 視圖。
2. 在 [連線] 視圖的底部, 按一下 [ **SQL Server Big Data**叢集] 將它展開。
3. 按一下 [**新增 SQL Server big data 叢集控制器**], 這將會啟動新的對話方塊。

## <a name="add-new-controller"></a>加入新的控制器

1. 新增您的叢集名稱。
2. 新增您的叢集管理服務 URL。 這可以在 BDC 儀表板的 [服務端點] 資料表中找到, 或詢問您的叢集系統管理員。
3. 新增您的使用者名稱和密碼。

## <a name="launch-controller-dashboard"></a>啟動控制器儀表板

1. 當您成功新增控制器時, 您可以在 SQL Server Big Data 叢集底下加以查看。
2. 若要啟動儀表板, 請在控制器上按一下滑鼠右鍵, 然後按一下 [**管理**]。

## <a name="controller-dashboard"></a>控制器儀表板

1. 在控制器儀表板上, 有3個主要元件:

    - 頂端的**工具列**, 其中包含儀表板的動作。
    - 左側導覽**窗格**, 會變更儀表板上的不同視圖。
    - 涵蓋大部分頁面的**視圖**。

2. 在 [ **Big data cluster 總覽**] 頁面上, 您可以看到:

    - 叢集**屬性**, 以查看您叢集的相關資訊。
    - 叢集**總覽**以查看所有叢集元件的高階總覽, 以及哪些狀況不良
    - 用來複製或存取 SQL Server Big Data 叢集中不同服務的**服務端點**。

3. 在 [流覽 **] 窗格中,** 您可以看到服務清單, 然後按一下其中一個來查看其他叢集詳細資料。 當您按一下 [叢集中的服務] 時, 這會是相同的視圖 **。**

4. 叢集**詳細資料**下的每個視圖都包含相同的 UI 元件:

    - **健全狀況狀態詳細資料**, 可共用元件的狀態和健全狀況狀態。
    - 透過 Grafana 和 Kibana 來查看其他計量和記錄的**計量和記錄**。

1. 如果您看到狀況不良的元件, 請按一下工具列上的 [**疑難排解**] 來啟動包含筆記本的 Jupyter 書籍, 以協助診斷問題。

## <a name="next-steps"></a>後續步驟

如需控制器的詳細資訊, 請參閱[我們的控制器檔](concept-controller.md)。