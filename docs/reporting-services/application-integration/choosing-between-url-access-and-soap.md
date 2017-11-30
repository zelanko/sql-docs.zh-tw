---
title: "在 Reporting Services 的 URL 存取與 SOAP 之間選擇 | Microsoft Docs"
ms.custom: 
ms.date: 10/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8d09ebc398462e9a79a0a107600b147c748125a7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="choosing-between-url-access-and-soap-in-reporting-services"></a>在 Reporting Services 的 URL 存取與 SOAP 之間選擇

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合到自訂應用程式頗具挑戰性。 不過，這個挑戰不是程式設計模型或是 API 的複雜性，而是有許多整合它的可能方法。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 是從無到有設計為開發人員平台，因此它是以程式設計彈性的考量所建立。 當要做出有關將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表導覽與管理功能整合至現有商務應用程式的重大決定時，彈性便會派上用場。

> [!NOTE]
> 從 SQL Server 2017 Reporting Services 開始，開發方案可使用 REST API 存取。 SOAP API 存取已被取代。 如需詳細資訊，請參閱[使用 Reporting Services 的 REST API 進行開發](../developer/rest-api.md)。
  
 將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合到自訂應用程式 URL 存取與 Reporting Services SOAP API，有兩種方法。 要使用哪個方法取決於多個因素。 在某些情況下，將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合到自訂商務應用程式，需要同時使用 URL 存取與 SOAP。 您應該問下列問題：  
  
-   您或您的使用者需要哪些類型的企業報表功能？ 您需要簡單的方法以啟動和導覽報表，或者您需要自訂商務解決方案有更進階的報表伺服器管理功能？  
  
-   使用者在操作時通常需要哪些類型的環境？ 商務應用程式是 Web 應用程式或 Windows 應用程式？ 使用者從 Win32 環境切換到 Web 環境有多容易？ 在執行和管理報表的環境中，您需要哪些類型的控制項？  
  
 一旦您已回答上述問題，即可決定如何將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合到 IT 基礎結構中。 通常，檢視和導覽個別報表時，較適合使用 URL 存取。 URL 存取可讓您隨心所欲且快速地導覽報表，而不會有 Web 服務的負擔。 此外，URL 存取是目前唯一為報表導覽使用完整 HTML 檢視器的程式設計技術。 此外，URL 存取提供比 SOAP 更佳的效能，因為它會略過對伺服器和來自伺服器之 SOAP 要求的封送處理。 在需要使用檢視和導覽內建工具來快速且輕鬆地存取報表的整合案例中，URL 存取是較佳的選擇。  
  
> [!NOTE]  
> 報表伺服器 URL 存取支援報表工具列的 HTML 檢視器與擴充功能。 SOAP API 並不支援這類型的轉譯報表。 如果您使用 SOAP API 轉譯報表，請設計和開發自己的報表工具列。
  
 如需報表工具列的詳細資訊，請參閱 [HTML 檢視器和報表工具列](../../reporting-services/html-viewer-and-the-report-toolbar.md)。  
  
 如需 URL 存取的詳細資訊，請參閱 [URL 存取](../../reporting-services/url-access-ssrs.md)。  
  
 URL 存取對於檢視報表非常有用，但是它並未提供可能對於任何企業報表案例很重要的報表與命名空間管理功能。 在此情況下，建議使用 Reporting Services SOAP API 的廣泛和豐富功能。 透過 SOAP API，您可以管理和部署報表、建立排程、設定伺服器屬性、管理報表伺服器命名空間、建立訂閱等等。 SOAP API 會在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中公開一組完整的管理功能。 SOAP API 也可以透過 API 的 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 方法啟用報表檢視和導覽。 不過，透過 SOAP API 檢視報表，並不會啟用報表工具列的內建檢視功能，也不會自動處理 URL 存取提供的報表互動功能。  
  
 如需 Reporting Services SOAP API 的詳細資訊，請參閱[報表伺服器 Web 服務](../../reporting-services/report-server-web-service/report-server-web-service.md)。  
  
 在大部分的情況下，將同時需要 URL 存取與 SOAP 呼叫，才能符合報表需求。 當初次連接到報表伺服器資料庫，並在使用者介面中提供可用的報表清單，而且使用 URL 存取來實際存取和導覽個別報表時，會使用 SOAP。  
  
 如需結合 URL 存取與 Web 服務以提供整合報表的範例，請參閱 [SQL Server Reporting Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=177889)。

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
