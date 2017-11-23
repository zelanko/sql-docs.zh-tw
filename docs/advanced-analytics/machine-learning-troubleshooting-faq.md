---
title: "疑難排解與 SQL Server 中的機器學習的常見問題集 |Microsoft 文件"
ms.custom: 
ms.date: 06/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e110a2578d6663c2c7c4c2e0dd92957744b44f4a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="troubleshoot-machine-learning"></a>機器學習的疑難排解

本文章提供有關安裝與設定的 SQL Server 中的機器學習功能的疑難排解資訊。 資訊包括設定指南、 已知的問題和版本資訊的連結。 其他文章連結至在此文件提供 SQL Server 中的機器學習解決方案的效能最佳化的相關建議。

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

+ [安裝 R 服務或使用 R 的機器學習服務](../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)
+ [設定機器學習服務，使用 Python](../advanced-analytics/python/setup-python-machine-learning-services.md)
+ [安裝程式常見問題集](../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [使用 SqlBindR 升級 R services 的執行個體](../advanced-analytics/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

下列文章描述離線安裝程式的 SQL Server 中的機器學習功能所需的額外步驟：

+ [自動的安裝的 R 服務](../advanced-analytics/r/unattended-installs-of-sql-server-r-services.md) 
+ [自動的安裝的機器學習服務，使用 Python](../advanced-analytics/python/unattended-installs-of-sql-server-python-services.md)

如果您要安裝的機器學習服務無法建立網際網路連線的電腦上的功能，請使用這份文件中的連結，再開始安裝程式下載的 R 和 Python 元件：

+ [在沒有網際網路存取的情況下安裝機器學習服務元件](../advanced-analytics/r/installing-ml-components-without-internet-access.md)

### <a name="configuration"></a>組態

下列文章包含預設值的相關資訊，以及如何自訂機器學習服務執行個體上的設定：

+ [修改 SQL Server R services 的使用者帳戶集區](../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [設定及管理進階的分析擴充功能](../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)  
+ [如何建立資源集區](r/how-to-create-a-resource-pool-for-r.md)
+ [適用於 R 工作負載最佳化](r/operationalizing-your-r-code.md)

## <a name="related-tools-and-services"></a>相關的工具和服務

+ [設定 Microsoft 機器學習伺服器獨立](../advanced-analytics/r/create-a-standalone-r-server.md)
+ [設定 Azure VM 上的 R 伺服器](../advanced-analytics/r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
+ [安裝 R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)
+ [取得 Visual Studio 的 R 工具](https://www.visualstudio.com/vs/rtvs/)
