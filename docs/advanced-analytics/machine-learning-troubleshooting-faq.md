---
title: 疑難排解
description: 提供解決已知問題的起點。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c9be3a8dff314f6645029fb54803ad30dc04db27
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727563"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>針對 SQL Server 中的機器學習進行疑難排解
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用本文作為解決已知問題的起點。

## <a name="known-issues"></a>已知問題

下列文章將說明目前和先前版本的已知問題：

+ [R Services 的已知問題](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 版本資訊](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>如何收集系統資訊

如果您遇到錯誤，或需要了解環境中的問題，請務必有系統地收集相關資訊。 下列文章提供有助於自行進行疑難排解的資訊清單，或提出技術支援的要求。

+ [針對機器學習的資料收集進行疑難排解](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>安裝和設定指南

如果您尚未使用 SQL Server 設定機器學習，或想要新增功能，請從這裡開始：

+ [安裝 SQL Server 機器學習服務 (資料庫內)](install/sql-machine-learning-services-windows-install.md)
+ [安裝 SQL Server Machine Learning Server (獨立式)](install/sql-machine-learning-standalone-windows-install.md)
+ [命令提示字元設定](install/sql-ml-component-commandline-install.md)
+ [離線安裝程式 (不連線到網際網路)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>組態

下列文章包含預設值的相關資訊，以及如何在執行個體上自訂機器學習的設定：

+ [在 SQL Server 機器學習服務中調整外部指令碼的平行執行](administration/modify-user-account-pool.md)   
+ [設定及管理進階分析擴充功能](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [如何建立資源集區](r/how-to-create-a-resource-pool-for-r.md)
+ [R 工作負載的最佳化](r/operationalizing-your-r-code.md)
