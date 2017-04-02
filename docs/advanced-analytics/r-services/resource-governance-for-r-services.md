---
title: "R 服務的資源管理 | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# R 服務的資源管理
  以程式碼的一個痛苦點是分析大量資料，在生產環境中需要額外的硬體，而且資料經常移動資料庫外部的電腦不受 IT。  若要執行進階的分析作業，客戶想要利用資料庫伺服器資源，並保護其資料，但需要這類作業都符合企業層級的相容性需求，例如安全性和效能。  
  
 本節提供有關如何管理和執行使用中的 R 工作 R 執行階段所使用的資源資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 做為計算內容的執行個體。  
  
## 資源管理是什麼？  
 資源控管被設計來識別並防止在資料庫伺服器環境，在經常會有多個相依的應用程式和多個服務以支援，並平衡中很常見的問題。 如 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，資源管理包含下列工作︰  
  
-   用來識別使用過多的伺服器資源的指令碼。  
  
     系統管理員需要能夠終止或節流會消耗過多資源的工作。  
  
-   減少非預期的工作負載。  
  
     比方說，如果伺服器上同時執行多個 R 工作，工作將無法彼此隔離的使用資源集區產生的資源爭用可能會導致無法預期的效能或威脅完成的工作負載。  
  
-   排列優先順序的工作負載。  
  
     系統管理員或架構設計人員必須要能夠指定工作負載，您必須有優先權，或確保資源爭用的情況是否完成特定工作負載。  
  
 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，您可以使用 [資源管理員](../../relational-databases/resource-governor/resource-governor.md) 來管理遠端 R 作業和 R 的執行階段所使用的資源。  
  
## 如何使用資源管理員來管理 R 工作  
 一般情況下，您可以管理資源配置到 R 工作，藉由建立 *外部的資源集區* 並將工作負載指派給集區或集區。 外部資源集區是一種全新的資源集區中導入 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ，以協助管理 R 執行階段和其他外部資料庫引擎處理程序。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ，現在有三種類型的預設資源集區。  
  
-    *內部集區* 代表資源使用 SQL Server 本身並無法改變或限制。  
  
-    *預設集區* 是可用來修改整個伺服器的資源使用的預先定義的使用者集區。 您也可以定義屬於此集區，來管理資源的存取權的使用者群組。  
  
-    *預設外部集區* 是外部資源的預先定義的使用者集區。 此外，您可以建立新的外部資源集區，並定義使用者群組，屬於此集區。  
  
 此外，您可以建立 *使用者定義的資源集區* 資源配置給資料庫引擎或其他應用程式，並建立 *使用者定義的外部資源集區* 管理 R 和其他外部處理序。  
  
 簡介術語和一般概念，請參閱 [資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)。  
  
> [!NOTE]  
>  新的資源管理員屬性是目前可用只能透過 DDL 陳述式或指令碼。無法使用中的使用者介面建立外部的資源群組 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。  
  
## 使用資源管理員的資源管理 

   如果您不熟悉資源管理員，請參閱本主題的如何修改執行個體的預設資源，並建立新的外部資源集區的快速逐步解說︰  [How To︰ 建立資源集區](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)   
  
 您可以使用 *外部的資源集區* 機制來管理下列 R 可執行檔所使用的資源︰  
  
-   Rterm.exe 和附屬程序  
  
-   BxlServer.exe 和附屬程序  
  
-   啟動的啟動列的附屬處理序  
  
 不過，直接管理的 [啟動列] 不支援使用資源管理員服務。 這是因為 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 是受信任的服務，根據設計可以裝載 Microsoft 所提供的啟動程式。 若要避免過度使用資源，也會設定受信任的啟動程式。  
  
 我們建議您管理使用資源管理員的附屬程序，並調整它們的個別資料庫組態和工作負載需求。  例如，任何個別的附屬程序可建立或終結依需求執行期間。  
  
## 停用外部指令碼執行  
 外部指令碼支援是選擇性在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式。 即使在安裝之後 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], 、 執行外部指令碼的功能預設是 OFF，而您必須手動重新設定此屬性，並重新啟動要啟用指令碼執行的執行個體。  
  
 因此，如果沒有資源問題需要立即降低或安全性問題，系統管理員可以立即使用停用任何外部指令碼執行 [sp_configure & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 設定屬性和 `external scripts enabled` 為 FALSE 或 0。  
  
## 另請參閱  
 [管理和監視 R 方案](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [如何︰ 建立資源集區](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  