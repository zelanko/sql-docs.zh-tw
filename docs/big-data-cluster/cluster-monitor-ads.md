---
title: 使用 Azure Data Studio 監視叢集
titleSuffix: SQL Server Big Data Clusters
description: 使用 Azure Data Studio 在 SQL Server 2019 巨量資料叢集上監視叢集。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4c4dc9956b8c3f9802feb839096195c09664d0d6
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378368"
---
# <a name="monitor-cluster-status-with-azure-data-studio"></a>使用 Azure Data Studio 監視叢集狀態

本文說明如何使用 Azure Data Studio 來檢視巨量資料叢集的狀態。

## <a name="use-azure-data-studio"></a><a id="datastudio"></a> 使用 Azure Data Studio

下載 [Azure Data Studio](https://aka.ms/getazuredatastudio) 的最新 **測試人員組建** 之後，您可以使用 SQL Server 巨量資料叢集儀表板來檢視服務端點和巨量資料叢集的狀態。 以下部分功能僅先在 Azure Data Studio 的測試人員組建中提供。

1. 首先，在 Azure Data Studio 中建立與您巨量資料叢集的連線。 如需詳細資訊，請參閱[使用 Azure Data Studio 連線至 SQL Server 巨量資料叢集](connect-to-big-data-cluster.md)。

1. 以滑鼠右鍵按一下巨量資料叢集端點，然後按一下 [管理]  。

   ![以滑鼠右鍵按一下 [管理]](media/view-cluster-status/right-click-manage.png)

1. 選取 [SQL Server 巨量資料叢集]  索引標籤以存取巨量資料叢集儀表板。

   ![巨量資料叢集儀表板](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>服務端點

能夠輕鬆存取巨量資料叢集中的各種服務十分重要。 巨量資料叢集儀表板提供服務端點資料表，可讓您查看並複製服務端點。

![服務端點](media/view-cluster-status/service-endpoints.png)

當您需要端點以連線至這些服務時，這些服務會列出可複製及貼上的端點。 例如，您可以按一下端點右側的複製圖示，然後將其貼入要求該端點的文字視窗中。 若要執行[叢集狀態筆記本](#notebook)，叢集管理服務端點是必要的。

### <a name="dashboards"></a>儀表板

服務端點資料表也會公開數個儀表板以進行監視：

- 計量 (Grafana)
- 記錄 (Kibana)
- Spark 作業監視
- Spark 資源管理

您可以直接按一下這些連結。 存取下列儀表板時，您必須進行驗證。 針對計量和記錄儀表板，請提供您在部署時使用 **AZDATA_USERNAME** 和 **AZDATA_PASSWORD** 環境變數所設定的控制器系統管理員認證。 Spark 儀表板將使用閘道 (Knox) 認證：可為叢集中與 AD 整合的 AD 身分識別，或 **AZDATA_USERNAME** 與 **AZDATA_PASSWORD** (若叢集中使用基本驗證)。

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

### <a name="cluster-status-notebook"></a><a id="notebook"></a> 叢集狀態筆記本

1. 您也可以藉由啟動 [叢集狀態] 筆記本來檢視巨量資料叢集的叢集狀態。 若要啟動筆記本，請按一下 [叢集狀態]  工作。

    ![啟動](media/view-cluster-status/cluster-status-launch.png)

2. 開始之前，您需要下列項目：

    - 巨量資料叢集名稱
    - 控制器使用者名稱
    - 控制器密碼
    - 控制器端點

    預設的巨量資料叢集名稱是 **mssql-cluster** (除非您在部署期間自訂名稱)。 您可以從 [服務端點] 資料表中的 [巨量資料叢集] 儀表板找到控制器端點。 端點會列為 **叢集管理服務** 。 如果您沒有認證資訊，請洽詢為您部署叢集的系統管理員。

3. 按一下頂端工具列上的 [執行資料格]  。

4. 遵循提示輸入您的認證。 在您為巨量資料叢集名稱、控制器使用者名稱和控制器密碼鍵入每個認證後，請按下 Enter。

    > [!Note]
    > 如果您沒有設定巨量資料的設定檔，系統會要求您提供控制器端點。 請鍵入或貼上控制器端點，然後按 Enter 鍵以繼續。

5. 如果您成功連線，筆記本其餘部分會顯示巨量資料叢集每個元件的輸出。 當您想要重新執行特定程式碼儲存格時，請將滑鼠停留在程式碼儲存格上，然後按一下 **執行** 圖示。


## <a name="next-steps"></a>後續步驟

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
