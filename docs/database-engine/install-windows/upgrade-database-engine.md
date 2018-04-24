---
title: 升級資料庫引擎 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
caps.latest.revision: 62
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 374112a5e8055645339d08e2f993886af55d9e1c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="upgrade-database-engine"></a>升級 Database Engine

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  本節中的文章可協助您將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫引擎從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
1.  [選擇 Database Engine 升級方法](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md) ：開始升級之前，您必須了解各種升級方法。 本文討論各種升級方法，以及每個升級方法所需的步驟。  
  
2.  [計劃和測試 Database Engine 升級計劃](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md) ：檢閱升級方法之後，您就可以開始為環境開發適當的升級方法，並接著測試該升級方法，再升級現有的環境。 本文討論如何開發升級計畫，並加以測試。  
  
3.  [完成資料庫引擎升級](../../database-engine/install-windows/complete-the-database-engine-upgrade.md)：將資料庫升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之後，還需要執行其他步驟，包括建立新備份、啟用新功能及重新填入全文檢索目錄。 本文會討論這些步驟。  
  
4.  [變更資料庫相容性模式並使用查詢存放區](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md) ：將資料庫升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之後所要執行的其中一個步驟是啟用新功能，方法是變更資料庫相容性模式，然後再使用查詢存放區來監視效能。 本文會討論這項程序，並提供建議的工作流程。  
  
5.  [善用新的 SQL Server 功能](http://www.microsoft.com/sql-server/sql-server-2017)：最後，完成上述步驟之後，您就可以開始探索如何利用特定新資料庫引擎增強。 本文提供其中一些增強功能的建議，以及詳細資訊的連結。  
  
  
