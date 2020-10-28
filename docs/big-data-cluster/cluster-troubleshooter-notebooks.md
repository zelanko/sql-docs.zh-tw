---
title: 使用 Jupyter 筆記本和 Azure Data Studio 針對巨量資料叢集 (BDC) 進行疑難排解
titleSuffix: SQL Server Big Data Clusters
description: 使用 Jupyter 筆記本和 Azure Data Studio 在 SQL Server 2019 巨量資料叢集上針對 BDC 進行疑難排解。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 073776c042c0a0da136347c8e1658603b755208f
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378369"
---
# <a name="troubleshooting-big-data-clusters-bdc-with-notebooks"></a>使用筆記本針對巨量資料叢集 (BDC) 進行疑難排解

此頁面是適用於 SQL Server 巨量資料叢集的筆記本索引。 這些可執行的筆記本 (.ipynb) 是針對 SQL Server 2019 所設計的，可協助針對巨量資料叢集進行疑難排解。

每個筆記本都設計為會檢查自己的相依性。 [執行所有資料格] 不是會順利完成，就是會引發例外狀況，並提供可供前往另一個筆記本的超連結提示以便解決遺失的相依性。 請遵循後續筆記本的提示超連結，按下 [執行所有資料格]，並在成功時返回原始筆記本，然後 [執行所有資料格]。

所有相依性都安裝好之後，若 [執行所有資料格] 失敗，則每個筆記本都會分析結果，並在可能的情況下，產生可供前往另一個筆記本的超連結提示，以進一步協助解決此問題。


## <a name="troubleshooting-big-data-cluster-bdc"></a>針對巨量資料叢集 (BDC) 進行疑難排解

本節包含一組筆記本，可用來從 SQL Server 巨量資料叢集 (BDC) 取得記錄。

|Name |描述 |
|---|---|---|---|
|TSG100 - 巨量資料叢集疑難排解員|概述有關針對巨量資料叢集 (BDC) 問題進行疑難排解的所有可用筆記本以及其使用時機  |
|TSG101 - SQL Server 疑難排解員|概述有關針對 SQL Server 問題進行疑難排解的所有可用筆記本以及其使用時機  |
|TSG102 - HDFS 疑難排解員|概述有關針對 HDFS 問題進行疑難排解的所有可用筆記本以及其使用時機  |
|TSG103 - Spark 疑難排解員|概述有關針對 Spark 問題進行疑難排解的所有可用筆記本以及其使用時機  |
|TSG104 - 控制疑難排解員|概述有關針對控制器問題進行疑難排解的所有可用筆記本以及其使用時機  |
|TSG105 - 閘道疑難排解員|概述有關針對 Knox 閘道問題進行疑難排解的所有可用筆記本以及其使用時機  |
|TSG106 - 應用程式疑難排解員|概述有關針對應用程式部署問題進行疑難排解的所有可用筆記本以及其使用時機  |



## <a name="diagnose-issues-from-big-data-clusters-bdc"></a>診斷來自巨量資料叢集 (BDC) 的問題

一組筆記本，可用於診斷巨量資料叢集的狀況和狀態。

|Name |描述 |
|---|---|---|---|
|TSG002 - CrashLoopBackoff|此 TSG 會連線到最後一次嘗試進入「執行中」狀態失敗的每個容器，並取得目前和先前的容器記錄。 這可用於針對 kubectl 取得 Pod 中所報告的 CrashLoopBackOff 問題進行偵錯。|
|TSG025 - FSM 瀏覽器 - 查詢控制器 FSM 狀態|使用此筆記本連線到控制器資料庫，並瀏覽有限狀態機器 (FSM) 狀態。 使用此筆記本來列出使用中的狀態機器，並識別停滯的工作流程。|
|TSG026 - 連線到資料集區節點 (以執行 T-SQL)|使用此筆記本連線到資料集區節點 (以執行 T-SQL)|
|TSG027 - 觀察叢集部署|使用此筆記本來觀察叢集部署，並提供指引來針對 SQL Server 巨量資料叢集的建立問題進行疑難排解。下列命令通常有助於查明根本原因。 |
|TSG029 - 在叢集中尋找傾印|使用此筆記本，以在巨量資料叢集中，從 SQL Server 或控制器等處理序尋找 coredump 和 minidump。|
|TSG032 - 所有容器的 CPU 和記憶體使用量|使用此筆記本來檢查所有容器的 CPU 和記憶體使用量。|
|TSG037 - 判斷裝載主要複本的主機集區 Pod|使用此筆記本來判斷已啟用主要集區高可用性時，裝載了巨量資料叢集主要複本的主要集區 Pod。|
|TSG044 - 在主要集區容器中執行 sqlcmd|使用此筆記本來直接透過 T-SQL 連線到主要集區節點。|
|TSG055 - 計算 Curl 至 Sparkhead 的時間|使用此筆記本來診斷步驟，以了解從控制器 Pod 到 Sparkhead Pod 的 Curl 回應時間。|
|TSG060 - 所有 BDC PVC 的磁碟區磁碟空間|使用此筆記本來連線到每個容器，並針對對應到巨量資料叢集 (BDC) 之每個永續性磁碟區宣告 (PVC) 的每個永續性磁碟區 (PV)，取得其已使用/可用的磁碟空間。|
|TSG078 - 叢集健康情況是否良好|使用此筆記本來檢查您的巨量資料叢集 (BDC) 是否狀況良好。|
|TSG079 - 產生控制器核心傾印|使用此筆記本來產生控制器核心傾印。|
|TSG086 - 在所有容器中執行 top|使用此筆記本在所有容器中執行 top。|
|TSG087 - 在 namenode Pod 上使用 hadoop fs CLI|使用此筆記本在 namenode Pod 上使用 hadoop fs CLI。|
|TSG108 - 檢視控制器升級 ConfigMap|使用此筆記本來針對使用 **azdata bdc upgrade** 執行巨量資料叢集升級時的失敗進行疑難排解。|
|TSG112 - Active Directory 預先部署檢查|使用此筆記本來驗證巨量資料叢集 (BDC) 設定對 Active Directory (AD) 部署有效。|
|TSG115 - Linux 上的 SQL Server 安全性記錄翻譯工具|使用此筆記本來針對 Linux 上的 SQL Server 剖析 secuirty.ldap 和 security.kerberos 記錄器所產生的記錄。 若要啟用這些記錄器，請在執行 Linux 上的 SQL Server 的電腦上，將下面這幾行放在 /var/opt/mssql/logger.ini 中。 注意：此檔案有區分大小寫。|
|TSG116 - SQL BDC 安全性支援記錄翻譯工具|使用此筆記本來剖析 SQL BDC 中的安全性支援服務所產生的記錄。 為了取得記錄，我們會從叢集複製偵錯記錄並將其解壓縮。 請遵循下列步驟 - 執行 “azdata bdc debug copy-logs -n <namespace> *”。這會建立數個 .tar.gz 檔案 - 解壓縮 debuglogs-* <namespace>-<date>-<time>.tar.gz 的內容。尋找儲存于 ./<namespace>/control-<…>/security-support/supervisol/log/secsupp-stderr---<…>.log 的安全性支援記錄。|
|TSG119 - Active Directory 部署後檢查|此筆記本的設計是為了在 AD 部署之後驗證您的 BDC 設定。 其會針對所有具有 dnsName 屬性的端點檢查其 DNS 項目是否存在，而且這些 DNS 項目應該是主機記錄，而不是別名 (亦即 A 記錄而非 CNAME 記錄)。此外，也會檢查已知的 AD 帳戶是否存在及是否已啟用，以及預期的 SPN 是否存在|






## <a name="repair-issues-from-big-data-clusters-bdc"></a>修復來自巨量資料叢集 (BDC) 的問題

一組筆記本，可用來修復 SQL Server 巨量資料叢集的已知情況和狀態。

|Name |描述 |
|---|---|---|---|
|TSG005 - 偵測到轉送迴圈|使用此筆記本來處理偵測到的轉送迴圈，因為公用程式 dnsmasq 可將本機 loopback 放置在 resolv.conf 中，這可能會造成控制器 Pod 在一開始的叢集部署期間進入 CrashLoopBackOff： https://askubuntu.com/questions/627899/nameserver-127-0-1-1-in-resolv-conf-wont-go-away|
|TSG011 - 重新啟動 sparkhistory 伺服器|使用此筆記本來重新啟動 sparkhistory 伺服器，因為 sparkhistory java 處理序可能會在啟動期間停止回應。 重新啟動 sparkhistory 伺服器 (supervisorctl restart sparkhistory) 可解決此問題。|
|TSG018 - 終止主要集區上的 sqlservr 處理序| 當 T-SQL 關機未成功重新循環 ./sqlservr 處理序時，請使用此筆記本。 請使用此筆記本來終止主要 sqlservr 處理序；./sqlservr 前端處理序會自動重新啟動該處理序。|
|TSG024 - Namenode 處於安全模式| 當 HDFS 自己進入安全模式時，請使用此筆記本。 例如，若存放集區中有太多的 Pod 回收速度過快，則可能會自動啟用 [安全] 模式。|
|TSG028 - 重新啟動所有存放集區節點上的節點管理員| 當需要重新啟動所有存放集區節點上的節點管理員時，請使用此筆記本。|
|TSG038 - 因文件遺失金鑰而導致 BDC 建立失敗| 當 BDC 因為 - doc 遺失金鑰而造成失敗時，請使用此筆記本。|
|TSG039 - 無效的物件名稱 'role_permissions'| 當由於 Knox gateway.log 中的角色權限而導致無效物件問題時，請使用此筆記本|
|TSG040 - 無法從控制器取得檔案名稱並發生錯誤| 從控制器取得檔案名稱時若遇到 504 閘道逾時，請使用此筆記本。|
|TSG041 - 無法建立新的非同步 I/O 內容 (增加 sysctl 的 fs.aio-max-nr)| 當無法建立新的非同步 I/O 內容 (增加 sysctl 的 fs.aio-max-nr) 時，請使用此筆記本。|
|TSG045 - 允許附加到此大小 VM 的資料磁碟數目上限 (AKS)| 當允許附加到此大小 VM 的資料磁碟數目上限 (AKS) 時，請使用此筆記本。|
|TSG047 - ConfigException - 只預期有一個具有名稱的物件| 當擁有的 ConfigException 只預期一個具有名稱的物件時，請使用此筆記本。|
|TSG048 - 部署在「等待控制器 Pod 啟動」時停滯| 當部署在「等待控制器 Pod 啟動」時停滯，請使用此筆記本。|
|TSG050 - 叢集建立停止回應，並顯示「等待磁碟區針對 Pod 附加或掛接時超過逾時」| 當叢集建立停止回應，並顯示「等待磁碟區針對 Pod 附加或掛接時超過逾時」時，請使用此筆記本。|
|TSG052 - 嘗試取得 master-svc DNS 失敗，將會再試一次| 當叢集建立停止回應，並顯示「等待磁碟區針對 Pod 附加或掛接時超過逾時」時，請使用此筆記本。|
|TSG057 - 啟動控制器服務 .System.TimeoutException 時失敗| 當啟動控制器服務並取得 System.TimeoutException 時，請使用此筆記本。|
|TSG067 - 無法完成 kube config 安裝程式| 當完成 kube 組態的設定失敗時，請使用此筆記本。|
|TSG074 - 刪除應用程式部署| 當刪除 BDC 叢集中的應用程式發生問題時，請使用此筆記本。|
|TSG075 - FailedCreatePodSandBox，因為 NetworkPlugin cni 無法設定 pod| 當因為 NetworkPlugin cni 無法設定 Pod 而收到 FailedCreatePodSandBox 例外狀況時，請使用此筆記本。|
|TSG080 - 使用 azdata 刪除 Spark 工作階段| 當您刪除 Spark 工作階段時遇到問題，請使用此筆記本。|
|TSG109 - 設定升級逾時| 當遇到 BDC 升級問題時，請使用此筆記本。|
|TSG110 - Azdata 傳回 ApiError| 當 Azdata 傳回 ApiError 時，請使用此筆記本。|

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md)。

