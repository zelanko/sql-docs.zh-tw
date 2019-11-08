---
title: 使用控制器儀表板，管理 SQL Server 巨量資料叢集
titleSuffix: Manage SQL Server big data cluster with controller dashboard
description: 使用來自 Azure Data Studio 的筆記本，來管理巨量資料叢集與進行疑難排解。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a78074b7e32df18de1308d2354d98079d074f9bf
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531936"
---
# <a name="manage-big-data-clusters-for-sql-server-controller-dashboard"></a>管理 SQL Server 控制器儀表板的巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

除了 **azdata** 與叢集狀態筆記本之外，另有一種方式可檢視 SQL Server 巨量資料叢集的狀態。 您現在可以透過 [連線]  呈現程式碼 (viewlet) 來新增 SQL Server 巨量資料叢集控制器。 這可讓您使用儀表板來檢視叢集的健康狀態。

![儀表板](media/manage-with-controller-dashboard/controller-dashboard.png)
## <a name="prerequisites"></a>Prerequisites

您必須滿足下列必要條件，才能啟動筆記本：

* 最新版的 [Azure Data Studio Insiders 組建](https://docs.microsoft.com/sql/big-data-cluster/deploy-big-data-tools?view=sqlallproducts-download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc) \(英文\)
* 在 Azure Data Studio 中安裝 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 延伸模組

除了上述條件外，SQL Server 2019 巨量資料叢集也需要：

* **azdata**
    - [Windows 安裝程式](deploy-install-azdata-installer.md)
    - [Linux 套件管理員](deploy-install-azdata-linux-package.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="add-sql-server-big-data-cluster-controller"></a>新增 SQL Server 巨量資料叢集控制器

1. 在左窗格中，按一下 [連線] 檢視。
2. 在 [連線] 檢視底部，按一下 [SQL Server 巨量資料叢集]  予以展開。
3. 按一下 [新增 SQL Server 巨量資料叢集控制器]  ，以啟動新的對話方塊。

## <a name="add-new-controller"></a>新增控制器

1. 新增您的叢集名稱。
2. 新增您的叢集管理服務 URL。 您可以在您 BDC 儀表板的服務端點表格中找到此 URL，也可以詢問您的叢集管理員。
3. 新增您的使用者名稱與密碼。

## <a name="launch-controller-dashboard"></a>啟動控制器儀表板

1. 當您成功新增控制器之後，就能在 SQL Server 巨量資料叢集進行檢視。
2. 若要啟動儀表板，請在控制器上按一下滑鼠右鍵，然後按一下 [管理]  。

## <a name="controller-dashboard"></a>控制器儀表板

1. 控制器儀表板上有 3 個主要元件：

    - 頂端的**工具列**，其中包含了可以對儀表板執行的動作。
    - 儀表板左側的**瀏覽窗格**會變更成不同的檢視。
    - **檢視**會涵蓋幾乎整個頁面。

2. [巨量資料叢集概觀]  頁面會顯示：

    - [叢集屬性]  ：顯示叢集的相關資訊。
    - [叢集概觀]  ：顯示所有叢集元件的概觀，並指出其中狀況不良的元件
    - [服務端點]  ：可複製到或存取 SQL Server 巨量資料叢集內的其他服務。

3. [瀏覽窗格]  會顯示服務清單；按一下其中一項服務，可檢視其他叢集詳細資料。 此檢視與您按一下 [叢集概觀]  中之服務時所顯示的檢視相同。

4. [叢集詳細資料]  下的每個檢視，都由相同的 UI 元件組成：

    - [健康狀態詳細資料]  共用元件的狀態與健康狀態。
    - [診斷記錄及計量]  可透過 Grafana 及 Kibana 檢視其他計量與記錄。

1. 當看到狀況不良的元件時，可按一下工具列上的 [疑難排解]  ，啟動包含筆記本的 Jupyter Book 來協助診斷問題。

## <a name="next-steps"></a>Next Steps

如需控制器的詳細資訊，請參閱[我們的控制器文件](concept-controller.md)。