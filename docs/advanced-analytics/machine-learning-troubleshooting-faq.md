---
title: 機器學習服務的疑難排解和常見問題
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0cd9b4808d361cdbfa661feb31134da46baec3de
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344985"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>針對 SQL Server 中的機器學習進行疑難排解
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用此頁面做為處理已知問題的起點。

**適用於：** SQL Server 2016 R Services, SQL Server 2017 Machine Learning 服務 (R 和 Python)

## <a name="known-issues"></a>已知問題

下列文章說明目前和先前版本的已知問題:

+ [R 服務的已知問題](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 版本資訊](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>如何收集系統資訊

如果您遇到錯誤, 或需要瞭解環境中的問題, 請務必有系統地收集相關資訊。 下列文章提供可協助進行自我協助疑難排解的資訊清單, 或技術支援的要求。

+ [機器學習服務疑難排解的資料收集](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>安裝和設定指南

如果您尚未使用 SQL Server 設定機器學習, 或如果您想要新增功能, 請從這裡開始:

+ [安裝 SQL Server 2017 Machine Learning 服務 (資料庫內)](install/sql-machine-learning-services-windows-install.md)
+ [安裝 SQL Server 2017 Machine Learning Server (獨立式)](install/sql-machine-learning-standalone-windows-install.md)
+ [安裝 SQL Server 2016 R Services (資料庫內)](install/sql-r-services-windows-install.md)
+ [安裝 SQL Server 2016 R Server (獨立式)](install/sql-r-standalone-windows-install.md)
+ [命令提示字元設定](install/sql-ml-component-commandline-install.md)
+ [離線安裝程式 (不連線到網際網路)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>組態

下列文章包含預設值的相關資訊, 以及如何在實例上自訂機器學習服務的設定:

+ [在 SQL Server Machine Learning 服務中調整外部腳本的並存執行](administration/modify-user-account-pool.md)   
+ [設定和管理 advanced analytics 擴充功能](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [如何建立資源集區](r/how-to-create-a-resource-pool-for-r.md)
+ [R 工作負載的優化](r/operationalizing-your-r-code.md)
