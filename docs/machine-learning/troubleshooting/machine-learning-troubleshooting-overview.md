---
title: 針對 SQL Server 中的機器學習進行疑難排解
description: 提供解決 SQL 機器學習中問題的起點。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 05/31/2018
ms.topic: troubleshooting
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 732a4c1c37367a6faa78dd3da9919fd1cec2f774
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178859"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>針對 SQL Server 中的機器學習進行疑難排解
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

使用此文章作為針對在使用 SQL Server 機器學習時所遇到問題進行疑難排解的起點。

## <a name="known-issues"></a>已知問題

下列文章將說明目前和先前版本的已知問題：

+ [R Services 的已知問題](known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 版本資訊](../../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 版本資訊](../../sql-server/sql-server-2017-release-notes.md)
+ [SQL Server 2019 版本資訊](../../sql-server/sql-server-version-15-release-notes.md)

## <a name="how-to-gather-system-information"></a>如何收集系統資訊

如果您遇到錯誤，或需要了解環境中的問題，請務必有系統地收集相關資訊。 下列文章提供有助於自行進行疑難排解的資訊清單，或提出技術支援的要求。

+ [針對機器學習的資料收集進行疑難排解](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>安裝和設定指南

如果您尚未使用 SQL Server 設定機器學習，或想要新增功能，請從這裡開始：

+ [安裝 SQL Server 機器學習服務 (資料庫內)](../install/sql-machine-learning-services-windows-install.md)
+ [安裝 SQL Server Machine Learning Server (獨立式)](../install/sql-machine-learning-standalone-windows-install.md)
+ [命令提示字元設定](../install/sql-ml-component-commandline-install.md)
+ [離線安裝程式 (不連線到網際網路)](../install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>組態

下列文章包含預設值的資訊，以及如何針對 SQL 執行個體上的機器學習自訂組態：

+ [在 SQL Server 機器學習服務中調整外部指令碼的平行執行](../administration/scale-concurrent-execution-external-scripts.md)   
+ [如何建立資源集區](../administration/create-external-resource-pool.md)
+ [R 工作負載的最佳化](../r/operationalizing-your-r-code.md)
