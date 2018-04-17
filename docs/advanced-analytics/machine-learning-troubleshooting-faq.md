---
title: 疑難排解與 SQL Server 中的機器學習的常見問題集 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 80d153baed382c95c85793e1605b700c2719e13c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="troubleshoot-machine-learning"></a>機器學習的疑難排解
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章提供設定指南、 已知的問題和版本資訊的疑難排解連結。 其他文章連結至在此文件提供 SQL Server 中的機器學習解決方案的效能最佳化的相關建議。

使用此頁面做為起點，尋找已知的問題、 一般安裝程式的問題和程序進行疑難排解。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務 （R 和 Python）

## <a name="known-issues"></a>已知問題

下列文件清單的目前版本中，已知的問題，或說明問題之前的版本：

+ [R Services 已知的問題](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 版本資訊](../sql-server/sql-server-2017-release-notes.md)

## <a name="troubleshooting-prerequisites"></a>疑難排解的必要條件

如果您遇到錯誤，或需要了解您的環境中的問題時，務必有系統地收集相關的資訊。 此資訊包括版本、 版本、 安全性內容，以及執行內容。

下列文章提供有助於進行疑難排解，進而自行排除的資訊或為要求的清單，如需技術支援。

+ [取得機器學習的疑難排解資料收集](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>安裝和設定指南

如果您尚未設定機器學習服務與 SQL Server，或如果您想要新增功能，請啟動這裡：

+ [安裝 SQL Server 2017 機器學習服務 （資料庫）](install/sql-machine-learning-services-windows-install.md)
+ [安裝 SQL Server 2017 機器學習伺服器 （獨立）](install/sql-machine-learning-standalone-windows-install.md)
+ [安裝 SQL Server 2016 R Services （資料庫）](install/sql-r-services-windows-install.md)
+ [安裝 SQL Server 2016R 伺服器 （獨立）](install/sql-r-standalone-windows-install.md)
+ [命令提示字元安裝](install/sql-ml-component-commandline-install.md)
+ [離線安裝程式 (不連線到網際網路)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>組態

下列文章包含預設值的相關資訊，以及如何自訂機器學習服務執行個體上的設定：

+ [修改 SQL Server R services 的使用者帳戶集區](r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [設定及管理進階的分析擴充功能](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [如何建立資源集區](r/how-to-create-a-resource-pool-for-r.md)
+ [適用於 R 工作負載最佳化](r/operationalizing-your-r-code.md)
