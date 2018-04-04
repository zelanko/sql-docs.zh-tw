---
title: "管理和監視的機器學習解決方案 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d455f22a-190f-4a28-9088-98a843cd5db2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 65398ab522f7a39aae08b1f438d2fa59291e4e8f
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2018
---
# <a name="managing-and-monitoring-machine-learning-solutions"></a>管理和監視的機器學習解決方案
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明在 SQL Server 機器學習服務與資料庫管理員想要開始使用 R 和 Python 解決方案相關的功能。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

## <a name="security"></a>Security

資料庫管理員必須提供資料存取，不只是資料科學家但各種報表開發人員、 商務分析師和商務資料取用者。 R （以及現在 Python） 至 SQL Server 的整合支援資料科學角色的資料庫系統管理員提供許多優點。

+ [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的架構會保護您資料庫的安全，並隔離 R 工作階段的執行與資料庫執行個體的操作。

+ 您可以指定有權執行 R 指令碼的對象，並確保 R 工作中使用的資料是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中所定義之相同安全性角色來管理。

+ 資料庫管理員可以使用角色來管理安裝 R 封裝和 R 和 Python 指令碼的執行。

如需詳細資訊，請參閱下列資源：

+ [SQL Server 中 R 執行階段的安全性考量](../../advanced-analytics/r/security-considerations-for-the-r-runtime-in-sql-server.md)

+ [R 安全性概觀](../r/security-overview-sql-server-r.md)

+ [Python 安全性概觀](../python/security-overview-sql-server-python-services.md)

+ [安裝和管理 R 封裝](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)

## <a name="configuration-and-management"></a>設定和管理

資料庫管理員必須將競爭專案和優先順序整合至單一窗口︰資料庫伺服器。 它們必須支援分析，同時維護操作和報告資料存放區的健全狀況。 機器學習服務與 SQL Server 的整合會提供許多優點，資料庫管理員，負責越來越重要的角色部署用於資料科學之有效基礎結構。

+ R 和 Python 的工作階段會執行不同的處理序，以確保您的伺服器會繼續如往常般執行，即使外部指令碼執行階段有問題。

+ 低權限之實體的使用者帳戶用來包含及隔離外部指令碼活動。

+ DBA 可以使用標準 SQL Server 資源的管理工具，來控制配置給 R 執行階段，以防止從大量計算危及整體伺服器效能的資源數量。

如需詳細資訊，請參閱下列資源：

+ [資源管理針對 R 服務](../r/resource-governance-for-r-services.md)

+ [設定及管理進階分析擴充功能](../r/configure-and-manage-advanced-analytics-extensions.md)
