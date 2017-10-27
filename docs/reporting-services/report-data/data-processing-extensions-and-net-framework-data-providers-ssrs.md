---
title: "資料處理延伸模組與.NET Framework Data Provider (SSRS) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reports [Reporting Services], data
- data processing extensions [Reporting Services]
- data providers [Reporting Services]
- data retrieval [Reporting Services]
- Reporting Services, data sources
- report data [Report Builder], accessing
ms.assetid: 42a5afb5-f4c8-4957-b1fd-77bf39afa5be
caps.latest.revision: 19
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 74e70cd67affe64f31076f362f36e813f3357f82
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="data-processing-extensions-and-net-framework-data-providers-ssrs"></a>資料處理延伸模組與 .NET Framework Data Provider (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組是與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]一起安裝的元件，它的設計目的是要從特定類型的資料來源擷取資料，以及提供額外功能來支援報表設計和報表處理。 A[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]資料提供者是一種元件可從[!INCLUDE[msCoName](../../includes/msconame-md.md)]或支援的協力廠商來源<xref:System.Data>介面可讓您擷取和修改從特定類型的資料來源的資料。  
  
## <a name="understanding-a-data-processing-extension"></a>了解資料處理延伸模組  
 A[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]資料處理延伸模組支援的子集<xref:System.Data>介面。 資料處理延伸模組只需要資料來源的唯讀存取權限，因此不會實作寫入和更新的介面。 每一個資料處理延伸模組都可以提供自訂功能來支援報表處理。 例如，資料處理延伸模組可支援以下類型的功能：  
  
-   分開管理認證與連接字串  
  
-   支援多重值參數  
  
-   擷取資料來源上所計算的伺服器彙總  
  
-   從資料來源擷取資料屬性及資料值  
  
## <a name="understanding-a-data-provider"></a>了解資料提供者  
 A[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]資料提供者 （有時稱為驅動程式） 支援一組標準的<xref:System.Data>介面，讀取、 寫入和更新資料來源上的資料。 當特定類型的資料來源沒有可用的資料處理延伸模組時，可以使用資料提供者。 市面上有許多可用的協力廠商標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者。  
  
 因為 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 具有可延伸的資料提供者架構，所以您可以建置自訂的資料處理延伸模組，以包含 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組所提供的額外功能。 如需詳細資訊，請參閱 [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)。 如需協力廠商資料處理延伸模組的資訊，請參閱協力廠商資料處理延伸模組所隨附的文件。  
  
> [!NOTE]  
>  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者或自訂的資料處理延伸模組必須經過安裝和註冊後，才能用來存取資料來源中的資料。 資料處理延伸模組必須在報表用戶端上安裝及註冊才能撰寫報表，而且必須安裝在報表伺服器上才能檢視發行的報表。 並非所有資料提供者的設計都是在伺服器環境下運作。 如需詳細資訊，請參閱[註冊標準 .NET Framework Data Provider &#40;SSRS&#41;](../../reporting-services/report-data/register-a-standard-net-framework-data-provider-ssrs.md) 和[部署資料處理延伸模組](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料處理延伸模組概觀](../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  

