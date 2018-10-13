---
title: 疑難排解與 SQL Server 中的機器學習服務的常見問題集 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: dc04f74c4db5c05840795caea87efb9b0001171c
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2018
ms.locfileid: "48877921"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>疑難排解 SQL Server 中的機器學習服務
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用此頁面做為起點，來處理透過已知的問題。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 Machine Learning 服務 （R 和 Python）

## <a name="known-issues"></a>已知問題

下列文章描述的目前和先前版本的已知的問題：

+ [R Services 已知的問題](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 版本資訊](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>如何蒐集系統資訊

如果您遇到錯誤，或需要了解您的環境中的問題時，務必有系統地收集相關的資訊。 下列文章提供有助於自助疑難排解的資訊或為要求的清單，如需技術支援。

+ [資料收集機器學習服務進行疑難排解](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>安裝和設定指南

如果您還沒有將機器學習服務與 SQL Server 設定，或如果您想要新增功能，請啟動這裡：

+ [安裝 SQL Server 2017 Machine Learning 服務 （資料庫）](install/sql-machine-learning-services-windows-install.md)
+ [安裝 SQL Server 2017 Machine Learning 伺服器 （獨立式）](install/sql-machine-learning-standalone-windows-install.md)
+ [安裝 SQL Server 2016 R Services （資料庫）](install/sql-r-services-windows-install.md)
+ [安裝 SQL Server 2016 R Server （獨立式）](install/sql-r-standalone-windows-install.md)
+ [命令提示字元安裝](install/sql-ml-component-commandline-install.md)
+ [離線安裝程式 (不連線到網際網路)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>組態

下列文章包含資訊的預設值，以及如何自訂機器學習服務執行個體上的組態：

+ [小數位數的同時執行的 SQL Server Machine Learning 服務中的外部指令碼](administration/modify-user-account-pool.md)   
+ [設定及管理進階的分析擴充功能](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [如何建立資源集區](r/how-to-create-a-resource-pool-for-r.md)
+ [適用於 R 工作負載最佳化](r/operationalizing-your-r-code.md)
