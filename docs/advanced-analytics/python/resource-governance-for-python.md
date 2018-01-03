---
title: "資源管理針對 Python |Microsoft 文件"
ms.custom: 
ms.date: 03/30/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f270c173922c4b444e1d48e465f3f650fc7438f5
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="resource-governance-for-python"></a>資源管理針對 Python

因為 Python 透過啟用相同的擴充性架構實作 SQL Server 2016 中的 R 語言，您可以使用現有的工具在 SQL Server，例如資源管理員、 Dmv，以及擴充的事件、 監視執行中的 PythonSQL Server 中的指令碼。

資源監管尤其會非常重要，因為分析大量資料，在生產環境中可以稅更進階的硬體。  若要避免資料移至電腦，不可能受管理或稽核資料庫之外，很重要，資料庫管理員配置足夠的資源的進階的分析作業。

本章節提供有關如何管理 Python 執行階段所使用的資源資訊以及監視使用的 Python 資源指令碼工作中執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。

> [!NOTE]
> Python 支援是 SQL Server 2017 中的新功能，而且只在發行前版本。 尋找推出的詳細資訊。
> 一般情況下，您可以監視任何外部指令碼，包括執行 Python 的其中一個，使用相同架構所提供的 SQL Server 2016 中的 R 指令碼資源控管。

## <a name="what-is-resource-governance"></a>什麼是「資源管理」？

「資源管理」是設計用來識別並防止資料庫伺服器環境中的常見問題，資料庫伺服器環境中通常需要支援及平衡多個相依的應用程式和多個服務。 對於 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 而言，資源管理包含下列工作：  

+ **識別使用過多的伺服器資源的指令碼**。 系統管理員需要能夠終止或節流使用過多資源的作業。

+ **緩和無法預期的工作負載**。 如果在伺服器上同時執行多個 Python 工作，而且工作不互相隔離使用資源集區，產生的資源爭用無法會導致無法預期的效能或威脅完成的工作負載。

+ **排列優先順序的工作負載**。 如果發生資源爭用，系統管理員或架構設計人員需要能夠指定必須優先處理的工作負載，或是保證特定工作負載能夠完成。

您可以使用[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)來管理外部執行階段所使用的資源。 這包括從遠端啟動終端機，但執行使用 SQL Server 電腦當成計算內容的 Python 指令碼。

> [!NOTE] 
> 在 Enterprise Edition 中使用資源管理員。

## <a name="how-to-use-resource-governor-to-manage-python-execution"></a>如何使用資源管理員來管理 Python 執行

一般情況下，您可以管理資源配置到任何外部指令碼工作，藉由建立*外部資源集區*並將工作負載指派給集區。 外部資源集區是資源集區可協助管理 R 執行階段和其他處理序外部的 database engine 的 SQL Server 2016 中引進的新類型。 它可以用來監視從 SQL Server 2017 Python 作業。

有三種類型的預設資源集區：

+ 「內部集區」代表 SQL Server 本身使用的資源，並且無法修改或限制。
+ 「預設集區」是預先定義的使用者集區，您可以用來修改資源以提供給整部伺服器使用。 您還可以定義屬於這個集區的使用者群組，以管理資源的存取。
+ 「預設外部集區」是預先定義的外部資源使用者集區。 此外，您可以建立新的外部資源集區，並定義屬於這個集區的使用者群組。

另外，您可以建立「使用者定義的資源集區」將資源配置給資料庫引擎或其他應用程式，以及建立「使用者定義的外部資源集區」來管理 R 和其他外部程序。

如需術語和一般概念的絕佳簡介，請參閱 [Resource Governor 資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)。

## <a name="resource-management-using-resource-governor"></a>使用 Resource Governor 進行資源管理

如果您不熟悉 Resource Governor，請參閱以下主題的快速逐步解說，了解如何修改執行個體預設資源，以及建立新的外部資源集區：[操作說明：建立 R 的資源集區](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)

您可以使用*外部資源集區*機制，管理下列支援的可執行檔所使用的資源：

+ Python35.exe 時呼叫從 SQL Server 或從遠端呼叫 SQL Server，成為遠端計算內容
+ BxlServer.exe 和附屬程序
+ 啟動 [啟動列] 例如 PythonLauncher.dll launchers

> [!NOTE]
> 不支援使用資源管理員的啟動控制板服務之直接管理。 這是因為 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 是受信任的服務，根據設計只能裝載 Microsoft 提供的啟動程式。 另外也會設定受信任的啟動程式，以避免過度使用資源。

建議您使用 Resource Governor 來管理附屬程序，並將它們微調以滿足個別資料庫組態和工作負載的需求。  例如，任何的個別附屬程序在執行期間都可依需求建立或終結。

## <a name="disable-or-enable-external-script-execution"></a>停用或啟用外部指令碼執行

外部指令碼支援是選擇性的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式中，而即使安裝完整的外部指令碼執行後會設定為 OFF 預設基於安全性理由。 因此，您已完成安裝的機器學習語言和相關的服務的其中一個之後，您必須明確地重新設定執行個體，然後重新啟動 database engine 服務。

萬一失控的指令碼，您可以停用所有的指令碼執行。 只要反向執行此程序，並將屬性設定`external scripts enabled`為 FALSE 或 0，執行個體上的。 這會立即停用任何外部指令碼執行。 您應該保留此選項的安全性問題，或在其中系統管理員需要立即以緩解資源問題的情況。

## <a name="see-also"></a>請參閱

[資源管理員資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)

