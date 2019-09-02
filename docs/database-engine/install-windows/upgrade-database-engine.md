---
title: 升級資料庫引擎 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: cff2727815c5cd6cada3d2111e0aada4e722f800
ms.sourcegitcommit: a1ddeabe94cd9555f3afdc210aec5728f0315b14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2019
ms.locfileid: "70122967"
---
# <a name="upgrade-database-engine"></a>升級 Database Engine

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
  本節中的文章可協助您將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫引擎從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
1.  [選擇資料庫引擎升級方法](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)。 開始升級之前，您必須了解各種升級方法。 本文討論各種升級方法，以及每個升級方法所需的步驟。  
  
2.  [計劃和測試資料庫引擎升級計畫](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)。 檢閱升級方法之後，您就可以開始為環境開發適當的升級方法，並接著測試該升級方法，再升級現有的環境。 本文討論如何開發升級計畫，並加以測試。  
  
3.  [完成資料庫引擎升級](../../database-engine/install-windows/complete-the-database-engine-upgrade.md)。 在您將資料庫升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 且資料庫上線後，還需要執行其他步驟，包括建立新備份、升級資料庫功能以啟用新功能，以及重新填入全文檢索目錄。 本文會討論這些步驟。  
  
4.  升級[資料庫相容性層級](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades) (**適用於：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)])。 在新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 的資料庫上線之後，可能需要採取的其中一個步驟是藉由變更資料庫相容性層級來升級資料庫功能模式，以啟用新功能。 這可以手動或透過查詢調整小幫手來完成。 

    - [變更資料庫相容性模式並使用查詢存放區](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)。 在手動變更資料庫相容性層級之後，請使用查詢存放區來監視效能並找出可能的迴歸。 本文會討論這項建議的程序，並提供建議的工作流程。  

    - [使用查詢調整小幫手變更資料庫相容性模式](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)。 或者，若要手動變更，請使用**查詢調整小幫手 (QTA)** ，讓其透過建議的程序引導您變更資料庫相容性層級。 本文會討論這項程序，並提供 QTA 工作流程的指示。  

    如需變更資料庫相容性層級後可用的新功能和改善行為詳細資訊，請參閱[相容性層級之間的差異](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-stored-procedures)。

5.  [利用新的 SQL Server 功能](https://www.microsoft.com/sql-server/sql-server-2017)。 最後，完成上述步驟之後，您就可以開始探索如何利用新資料庫引擎的特定增強功能。 本文提供其中一些增強功能的建議，以及詳細資訊的連結。  
  
  
