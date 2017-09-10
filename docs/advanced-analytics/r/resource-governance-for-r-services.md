---
title: "R Services 的資源管理 | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5475c2258971c48c2e19bba69d9ec962ae48be87
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="resource-governance-for-r-services"></a>R Services 的資源管理
  R 的一個痛苦點是在生產環境中分析大量資料時需要額外的硬體，而且資料經常會移到資料庫外部不受 IT 控制的電腦。  為了執行進階的分析作業，客戶會想利用資料庫伺服器資源，而且為了保護他們的資料，他們會要求這類作業符合企業級的合規性需求，例如安全性及效能。  
  
 本節提供如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體當作計算內容，管理 R 執行階段和 R 作業執行所使用之資源的相關資訊。  
  
## <a name="what-is-resource-governance"></a>什麼是「資源管理」？  
 「資源管理」是設計用來識別並防止資料庫伺服器環境中的常見問題，資料庫伺服器環境中通常需要支援及平衡多個相依的應用程式和多個服務。 對於 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 而言，資源管理包含下列工作：  
  
-   識別使用過多伺服器資源的指令碼。  
  
     系統管理員需要能夠終止或節流使用過多資源的作業。  
  
-   減少無法預期的工作負載。  
  
     例如，如果在伺服器上同時執行多個 R 作業，而作業並未使用資源集區彼此隔離，則造成的資源爭用會導致無法預期的效能，或威脅工作負載的完成。  
  
-   排列工作負載優先順序。  
  
     如果發生資源爭用，系統管理員或架構設計人員需要能夠指定必須優先處理的工作負載，或是保證特定工作負載能夠完成。  
  
 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中，您可以使用 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) 來管理 R 執行階段和遠端 R 作業使用的資源。  
  
## <a name="how-to-use-resource-governor-to-manage-r-jobs"></a>如何使用 Resource Governor 管理 R 作業  
 通常，您會建立「外部資源集區」來管理配置給 R 作業的資源，並將工作負載指派到集區。 外部資源集區是在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中導入的新型資源集區，可協助管理 R 執行階段和資料庫引擎外部的其他程序。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，現在有三種預設資源集區類型。  
  
-   「內部集區」代表 SQL Server 本身使用的資源，並且無法修改或限制。  
  
-   「預設集區」是預先定義的使用者集區，您可以用來修改資源以提供給整部伺服器使用。 您還可以定義屬於這個集區的使用者群組，以管理資源的存取。  
  
-   「預設外部集區」是預先定義的外部資源使用者集區。 此外，您可以建立新的外部資源集區，並定義屬於這個集區的使用者群組。  
  
 另外，您可以建立「使用者定義的資源集區」將資源配置給資料庫引擎或其他應用程式，以及建立「使用者定義的外部資源集區」來管理 R 和其他外部程序。  
  
 如需術語和一般概念的絕佳簡介，請參閱 [Resource Governor 資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)。  

  
## <a name="resource-management-using-resource-governor"></a>使用 Resource Governor 進行資源管理 

   如果您不熟悉 Resource Governor，請參閱以下主題的快速逐步解說，了解如何修改執行個體預設資源，以及建立新的外部資源集區：[操作說明：建立 R 的資源集區](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)   
  
 您可以使用「外部資源集區」機制來管理下列 R 可執行檔使用的資源：  
  
-   Rterm.exe 和附屬程序  
  
-   BxlServer.exe 和附屬程序  
  
-   LaunchPad 啟動的附屬程序  
  
 不過，不支援使用 Resource Governor 直接管理 Launchpad 服務。 這是因為 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 是受信任的服務，根據設計只能裝載 Microsoft 提供的啟動程式。 另外也會設定受信任的啟動程式，以避免過度使用資源。  
  
 建議您使用 Resource Governor 來管理附屬程序，並將它們微調以滿足個別資料庫組態和工作負載的需求。  例如，任何的個別附屬程序在執行期間都可依需求建立或終結。  
  
## <a name="disable-external-script-execution"></a>停用外部指令碼執行  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式中對外部指令碼的支援是選擇性的。 即使安裝 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 之後，執行外部指令碼的功能預設值還是 OFF (關閉)，而您必須手動重新設定屬性，並重新啟動執行個體才能啟用指令碼執行。  
  
 因此，如果有需要立即減輕的資源問題或安全性問題，系統管理員可以立即停用任何的外部指令碼執行，方法是使用 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 並將屬性 `external scripts enabled` 設定為 FALSE 或 0。  
  
## <a name="see-also"></a>另請參閱  
 [管理和監視 R 方案](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [操作說明：建立 R 的資源集區](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [Resource Governor 資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  


