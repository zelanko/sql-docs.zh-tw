---
title: 巨量資料叢集 (BDC) 的系統管理資源
titleSuffix: SQL Server
description: 本文說明如何使用 Azure Data Studio、筆記本和 Azure Data CLI (azdata) 命令來檢視巨量資料叢集的狀態。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 10/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d469d1b8d89b07748485c9df3f7f7905af52099
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358156"
---
# <a name="administration-resources-for-big-data-clusters-bdc"></a>巨量資料叢集 (BDC) 的系統管理資源 

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文說明如何從的外部管理 SQL Server 巨量資料叢集。

## <a name="know-your-architecture"></a>了解您的架構

從 SQL Server 2019 (15.x) 開始，SQL Server 巨量資料叢集可讓您部署在 Kubernetes 上執行的 SQL Server、Spark 和 HDFS 容器可調整叢集。 下列文章概要說明巨量資料叢集：
- [什麼是 SQL Server 巨量資料叢集](big-data-cluster-overview.md)

SQL Server 巨量資料叢集可提供一致的授權和驗證。 下列文章概要說明巨量資料叢集的安全性：
- [SQL Server 巨量資料叢集的安全性概念](concept-security.md)

## <a name="manage-and-operate-with-tools"></a>管理和操作工具

下列文章說明如何以下列方式管理和操作巨量資料叢集： 

- [使用 Azure Data Studio 連線到 SQL Server 巨量資料叢集](connect-to-big-data-cluster.md)
- [管理 SQL Server 控制器儀表板的巨量資料叢集](manage-with-controller-dashboard.md)
- [使用 Azure Data Studio 筆記本管理 SQL Server 巨量資料叢集](notebooks-manage-bdc.md)
- [使用筆記本管理巨量資料叢集 (BDC) 叢集](cluster-manage-notebooks.md)
- [執行使用 Spark 的範例筆記本](notebooks-tutorial-spark.md)

## <a name="monitor-with-tools"></a>使用工具來監視

下列文章說明如何以下列方式監視巨量資料叢集： 

- [使用 Azure Data Studio 監視 BDC 叢集](cluster-monitor-ads.md)
- [使用 Azdata 公用程式監視 BDC 叢集](cluster-monitor-cmdlet.md)
- [使用 Grafana 儀表板監視 BDC 叢集](cluster-monitor-grafana.md)
- [使用 Jupyter 筆記本和 Azure Data Studio 監視 BDC 叢集](cluster-monitor-notebooks.md)

## <a name="monitor-and-inspect-logs-with-notebooks"></a>使用筆記本監視和檢查記錄

下列文章列出 Azure Data Studio 中可用的許多 Jupyter 筆記本。

- [使用筆記本監視叢集](cluster-monitor-notebooks.md)
- [使用筆記本收集和分析叢集中的記錄](cluster-logging-notebooks.md)

## <a name="big-data-clusters-troubleshooting-resources"></a>巨量資料叢集的疑難排解資源

下列文章說明如何針對巨量資料叢集進行疑難排解：

- [使用 kubectl 公用程式針對 BDC 叢集進行疑難排解](cluster-troubleshooting-commands.md) 
- [針對 pyspark 筆記本進行疑難排解](troubleshoot-pyspark-notebook.md)
- [使用 Jupyter 筆記本和 Azure Data Studio (ADS) 針對 BDC 叢集進行疑難排解](cluster-troubleshooter-notebooks.md)
- [還原 HDFS 權限](troubleshoot-hdfs-restore-admin.md)

下列文章說明如何針對在 Active Directory 模式中部署的巨量資料叢集進行疑難排解：
- [針對 Active Directory 模式中的 BDC 叢集進行疑難排解](troubleshoot-active-directory.md) 
- [針對 AD 模式登入失敗進行疑難排解](troubleshoot-ad-login-failed-untrusted-domain.md)
- [針對 BDC AD 模式部署已停止進行疑難排解](troubleshoot-ad-reverse-lookup-zone.md)

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md)。