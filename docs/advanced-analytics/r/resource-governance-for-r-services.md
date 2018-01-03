---
title: "資源管理針對 SQL Server 中的機器學習 |Microsoft 文件"
ms.custom: 
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 61cffc85e6a27ffe4c171da8849d84a19332f223
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>SQL Server 中的機器學習資源管理

本文章提供 SQL Server 中的功能，幫助配置和 R 和 Python 指令碼所使用的資源之間取得平衡的資源管理的概觀。

**適用於：** [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] 
 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]和[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]

## <a name="goals-of-resource-governance-for-machine-learning"></a>機器學習資源控管的目標

機器學習語言，例如 R 和 Python 已知的痛苦點就是資料庫以外，經常會將資料移電腦不受 IT。 另一個是 R 是單一執行緒，這表示，您可以只使用記憶體中可用的資料。 

SQL Server 機器學習服務可以減輕這些這兩個問題，並協助您符合企業法規遵循需求。 它會保留在資料庫中，進階的分析，並透過串流處理和區塊處理作業等功能的大型資料集上支援增加的效能。 不過，移動資料庫內部 R，並將 Python 計算會影響其他服務所使用的資料庫，包括一般使用者查詢、 外部應用程式，以及排程的資料庫作業的效能。

本節提供有關如何管理外部執行階段，例如 R 和 Python，用來減少影響其他核心資料庫的服務上的資源資訊。 資料庫伺服器環境通常為多個相依的應用程式和服務的中樞。

您可以使用[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)來管理外部執行階段所使用的 R，並將 Python 的資源。  機器學習資源管理機制會包含下列工作：

+ 識別使用過多伺服器資源的指令碼。
  
     系統管理員需要能夠終止或節流使用過多資源的作業。
  
+ 減少無法預期的工作負載。
  
     例如，如果在伺服器上同時執行多個機器學習工作，產生的資源爭用無法會導致無法預期的效能或威脅完成的工作負載。 不過，如果資源集區使用時，工作可以互相隔離。
  
-   排列工作負載優先順序。
  
     系統管理員或架構設計人員必須能夠將指定的工作負載，必須優先，或是保證資源競爭時，必須完成某些工作負載。

## <a name="how-to-use-resource-governor-to-manage-machine-learning"></a>如何使用資源管理員來管理機器學習服務
 
管理資源配置給 R 或 Python 的工作階段中，藉由建立*外部資源集區*，並將工作負載指派給集區或集區。 外部資源集區是資源集區中導入的新類型[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]可協助管理 R 執行階段和其他處理外部到 database engine。

SQL Server 支援三種類型的預設資源集區： 
  
-   「內部集區」代表 SQL Server 本身使用的資源，並且無法修改或限制。
  
-   「預設集區」是預先定義的使用者集區，您可以用來修改資源以提供給整部伺服器使用。 您還可以定義屬於這個集區的使用者群組，以管理資源的存取。
  
-   「預設外部集區」是預先定義的外部資源使用者集區。 此外，您可以建立新的外部資源集區，並定義屬於這個集區的使用者群組。
  
 另外，您可以建立「使用者定義的資源集區」將資源配置給資料庫引擎或其他應用程式，以及建立「使用者定義的外部資源集區」來管理 R 和其他外部程序。
  
 如需術語和一般概念的絕佳簡介，請參閱 [Resource Governor 資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)。

  
## <a name="resource-management-walkthrough-with-resource-governor"></a>資源管理逐步解說向資源管理員

如果您不熟悉資源管理員，請參閱本主題適用於快速如何修改預設執行個體的資源，並建立新的外部資源集區的逐步解說：[建立外部指令碼的資源集區](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)
  
 您可以使用*外部資源集區*機制，管理機器學習中使用下列可執行檔所使用的資源：

+ Rterm.exe 和附屬程序
+ Python.exe 和附屬程序
+ BxlServer.exe 和附屬程序
+ 啟動控制板啟動附屬處理序
  
> [!NOTE]
> 
> 不支援使用資源管理員的啟動控制板服務之直接管理。 這是因為 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 是受信任的服務，根據設計只能裝載 Microsoft 提供的啟動程式。 信任的 launchers 被設定來避免過度使用資源。
>   
> 建議您使用 Resource Governor 來管理附屬程序，並將它們微調以滿足個別資料庫組態和工作負載的需求。  例如，任何的個別附屬程序在執行期間都可依需求建立或終結。
  
## <a name="disable-external-script-execution"></a>停用外部指令碼執行

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式中對外部指令碼的支援是選擇性的。 即使在安裝之後機器學習功能，執行外部指令碼的功能預設是 OFF，而您必須手動重新設定屬性，並重新啟動以啟用指令碼執行的執行個體。

因此，如果需要立即緩解資源問題或安全性問題，系統管理員可以立即使用停用任何外部指令碼執行[sp_configure &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)並設定的屬性`external scripts enabled`為 FALSE 或 0。
  
## <a name="see-also"></a>另請參閱

[管理及監視機器學習服務方案](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

[建立機器學習的資源集區](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

[資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
