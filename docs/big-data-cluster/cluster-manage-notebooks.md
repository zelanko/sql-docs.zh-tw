---
title: 使用 Jupyter 筆記本和 Azure Data Studio 管理巨量資料叢集 (BDC)
titleSuffix: SQL Server Big Data Clusters
description: 使用 Jupyter 筆記本和 Azure Data Studio 在 SQL Server 2019 巨量資料叢集上管理巨量資料叢集 (BDC)。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e549a8005144e85a20cf613ff6695d11f7ff030f
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378365"
---
# <a name="manage-big-data-clusters-bdc-the-cluster-with-notebooks"></a>使用筆記本管理巨量資料叢集 (BDC) 叢集

此頁面是適用於 SQL Server 巨量資料叢集的筆記本索引。 這些可執行的筆記本 (.ipynb) 是針對 SQL Server 2019 所設計的，可協助管理巨量資料叢集。

每個筆記本都設計為會檢查自己的相依性。 [執行所有資料格] 不是會順利完成，就是會引發例外狀況，並提供可供前往另一個筆記本的超連結提示以便解決遺失的相依性。 請遵循後續筆記本的提示超連結，按下 [執行所有資料格]，並在成功時返回原始筆記本，然後 [執行所有資料格]。

所有相依性都安裝好之後，若 [執行所有資料格] 失敗，則每個筆記本都會分析結果，並在可能的情況下，產生可供前往另一個筆記本的超連結提示，以進一步協助解決此問題。


## <a name="installing-and-uninstalling-utilities-on-big-data-cluster-bdc"></a>在巨量資料叢集 (BDC) 上安裝和解除安裝公用程式

本節包含一組實用筆記本，可供您安裝和解除安裝命令列工具以及要管理 SQL Server 巨量資料叢集所需的套件。

|Name |描述 |
|---|---|---|---|
|SOP010 - 升級巨量資料叢集|使用此筆記本以透過 azdata 升級巨量資料叢集。 |
|SOP012 - 安裝適用於 Mac 的 unixodbc|在使用 brew 安裝 SQL Server 的 odbc 時如果收到錯誤，請使用此筆記本。|
|SOP036 - 安裝 kubectl 命令列介面|無論您的作業系統為何，都可以使用此筆記本來安裝 kubectl 命令列介面。|
|SOP037 - 解除安裝 kubectl 命令列介面|無論您的作業系統為何，都可以使用此筆記本來解除安裝 kubectl 命令列介面。|
|SOP038 - 安裝 Azure 命令列介面|無論您的作業系統為何，都可以使用此筆記本來安裝 Azure CLI 命令列介面。|
|SOP039 - 解除安裝 Azure 命令列介面|無論您的作業系統為何，都可以使用此筆記本來解除安裝 Azure CLI 命令列介面。|
|SOP040 - 在 ADS Python 沙箱中升級 pip|使用此筆記本在 ADS Python 沙箱中升級 pip。|
|SOP054 - 安裝 azdata 命令列介面|無論您的作業系統為何，都可以使用此筆記本來安裝 azdata 命令列介面。|
|SOP055 - 解除安裝 azdata 命令列介面|無論您的作業系統為何，都可以使用此筆記本來解除安裝 azdata 命令列介面。|
|SOP059 - 安裝 Kubernetes Python 模組|使用此筆記本以 Python 安裝 Kubernetes 模組。|
|SOP060 - 解除安裝 kubernetes 模組|使用此筆記本以 Python 解除安裝 Kubernetes 模組。|
|SOP061 - 刪除巨量資料叢集|使用此筆記本來刪除 BDC 叢集。|
|SOP062 - 安裝 ipython-sql 和 pyodbc 模組|使用此筆記本來安裝 ipython-sql 和 pyodbc 模組。|
|SOP063 - 安裝 azdata CLI (使用套件管理員)|使用此筆記本來安裝 azdata CLI (使用套件管理員)。|
|SOP064 - 解除安裝 azdata CLI (使用套件管理員)|使用此筆記本來解除安裝 azdata CLI (使用套件管理員)。|
|SOP069 - 安裝 ODBC for SQL Server|使用此筆記本來安裝 ODBC 驅動程式，因為 azdata 中的某些子命令需要 SQL Server ODBC 驅動程式。|


## <a name="managing-certificates-on-big-data-clusters-bdc"></a>在巨量資料叢集 (BDC) 上管理憑證

一組筆記本，可供執行筆記本以在巨量資料叢集上管理憑證。

|Name |描述 |
|---|---|---|---|
|CER001 - 產生根 CA 憑證|產生根 CA 憑證。 針對每個環境中的所有非生產叢集，請考慮使用一個根 CA 憑證，因為這項技術可減少需要上傳到用戶端 (其會連線到這些叢集) 的根 CA 憑證數目。 |
|CER002 - 下載現有的根 CA 憑證|使用此筆記本從叢集下載產生的根 CA 憑證。|
|CER003 - 上傳現有的根 CA 憑證|CER003 - 上傳現有的根 CA 憑證。|
|CER004 - 下載和上傳現有的根 CA 憑證|下載和上傳現有的根 CA 憑證。 |
|CER010 - 在本機安裝產生的根 CA|此筆記本會從本機 (從巨量資料叢集) 複製所產生的根 CA 憑證，此憑證是使用 **CER001 - 產生根 CA 憑證** 或 **CER003 - 上傳現有的根 CA 憑證** 進行安裝的，然後再將根 CA 憑證安裝到這部電腦的本機憑證存放區中。|
|CER020 - 建立管理 Proxy 憑證|此筆記本會建立管理 Proxy 端點的憑證。|
|CER021 - 建立 Knox 憑證|此筆記本會建立 Knox 閘道端點的憑證。|
|CER022 - 建立應用程式 Proxy 憑證|此筆記本會建立應用程式部署 Proxy 端點的憑證。|
|CER023 - 建立主要憑證|此筆記本會建立主要端點的憑證。|
|CER030 - 使用產生的 CA 簽署管理 Proxy 憑證|此筆記本會使用透過 **CER001 - 產生根 CA 憑證** 或 **CER003 - 上傳現有的根 CA 憑證** 所建立的產生根 CA 憑證，來簽署使用 **CER020 - 建立管理 Proxy 憑證** 所建立的憑證|
|CER031 - 使用產生的 CA 簽署 Knox 憑證|此筆記本會使用透過 **CER001 - 產生根 CA 憑證** 或 **CER003 - 上傳現有的根 CA 憑證** 所建立的產生根 CA 憑證，來簽署使用 **CER021 - 建立 Knox 憑證** 所建立的憑證|
|CER032 - 使用產生的 CA 簽署應用程式 Proxy 憑證|此筆記本會使用透過 **CER001 - 產生根 CA 憑證** 或 **CER003 - 上傳現有的根 CA 憑證** 所建立的產生根 CA 憑證，來簽署使用 **CER022 - 建立應用程式 Proxy 憑證** 所建立的憑證。|
|CER033 - 使用產生的 CA 簽署主要憑證|此筆記本會使用透過 **CER001 - 產生根 CA 憑證** 或 **CER003 - 上傳現有的根 CA 憑證** 所建立的產生根 CA 憑證，來簽署使用 **CER023 - 建立主要憑證** 所建立的憑證。|
|CER040 - 安裝已簽署的管理 Proxy 憑證|此筆記本會將使用 **CER030 - 使用產生的 CA 簽署管理 Proxy 憑證** 所簽署的憑證安裝到巨量資料叢集。|
|CER041 - 安裝已簽署的 Knox 憑證|此筆記本會將使用 **CER031 - 使用產生的 CA 簽署 Knox 憑證** 所簽署的憑證安裝到巨量資料叢集。|
|CER042 - 安裝已簽署的應用程式 Proxy 憑證|此筆記本會將使用 **CER032 - 使用產生的 CA 簽署應用程式 Proxy 憑證** 所簽署的憑證安裝到巨量資料叢集。|
|CER043 - 安裝已簽署的控制器憑證|此筆記本會將使用 **CER034 - 使用叢集根 CA 簽署控制器憑證** 所簽署的憑證安裝到巨量資料叢集，並請注意，此筆記本的結尾將會重新啟動控制器 Pod 以及所有使用 PolyBase 的 Pod (主要集區和計算集區 Pod) 以載入新的憑證。|
|CER050 - 等候 BDC 狀況良好|在重新啟動控制器 Pod 以及使用 PolyBase 的 Pod 以載入新的憑證之後，此筆記本會等到巨量資料叢集恢復健全狀態。|
|CER100 - 使用自我簽署憑證來設定叢集|此筆記本會在巨量資料叢集中產生新的根 CA，並為每個端點建立新的憑證 (這些端點包括：管理、閘道、應用程式 Proxy 和控制器)。 請使用新產生的根 CA 簽署每個新的憑證，但控制器憑證除外 (其是使用現有的叢集根 CA 所簽署的)，然後將每個憑證安裝到巨量資料叢集。 將新產生的根 CA 下載到這部電腦的「信任的根憑證授權單位」憑證存放區。 所有產生的自我簽署憑證都會儲存在控制器 Pod 的 test_cert_store_root 位置。|
|CER101 - 使用現有的根 CA 透過自我簽署憑證來設定叢集|此筆記本會使用巨量資料叢集內現有的已產生根 CA (已使用 **CER003** 加以上傳)，並為每個端點 (管理、閘道、應用程式 Proxy 和控制器) 建立新的憑證，然後使用新產生的根 CA 簽署每個新憑證，但控制器憑證除外 (其是使用現有的叢集根 CA 所簽署的)，然後將每個憑證安裝到巨量資料叢集。 所有產生的自我簽署憑證都會儲存在控制器 Pod 中 (位於 test_cert_store_root 位置)。 完成此筆記本之後，所有從這部電腦 (以及安裝了新根 CA 的任何電腦) 對巨量資料叢集的 https:// 存取都會顯示為安全。 ＜筆記本執行器＞章節會確保為了執行 App-Deploy 而建立的 CronJobs (OPR003) 將會安裝叢集根 CA，以便能安全地取得 JWT 權杖和 swagger.json。|

## <a name="backup-and-restore-from-big-data-cluster-bdc"></a>從巨量資料叢集 (BDC) 備份和還原

本節包含一組實用筆記本，可用來進行 SQL Server 巨量資料叢集的備份和還原作業。

| Name | 描述 |
|--|--|
| SOP008 - 使用 distcp 將 HDFS 檔案備份到 Azure Data Lake Store Gen2 | 此標準作業程序 (SOP) 會將資料從來源 SQL Server 2019 BDC 叢集的 HDFS 檔案系統，備份到您指定的 Azure Data Lake Store Gen2 帳戶。 請確定所設定的 Azure Data Lake Store Gen2 帳戶已啟用 [階層命名空間]。 |

## <a name="next-steps"></a>後續步驟

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
