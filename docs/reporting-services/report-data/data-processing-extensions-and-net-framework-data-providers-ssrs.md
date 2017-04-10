---
title: "資料處理延伸模組與 .NET Framework Data Provider (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "報表 [Reporting Services], 資料"
  - "資料處理延伸模組 [Reporting Services]"
  - "資料提供者 [Reporting Services]"
  - "資料擷取 [Reporting Services]"
  - "Reporting Services, 資料來源"
  - "報表資料 [報表產生器], 存取"
ms.assetid: 42a5afb5-f4c8-4957-b1fd-77bf39afa5be
caps.latest.revision: 19
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 19
---
# 資料處理延伸模組與 .NET Framework Data Provider (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組是與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]一起安裝的元件，它的設計目的是要從特定類型的資料來源擷取資料，以及提供額外功能來支援報表設計和報表處理。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 或支援 <xref:System.Data> 介面的協力廠商所提供的元件，讓您可以從特定類型的資料來源擷取和修改資料。  
  
## 了解資料處理延伸模組  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組支援 <xref:System.Data> 介面的子集。 資料處理延伸模組只需要資料來源的唯讀存取權限，因此不會實作寫入和更新的介面。 每一個資料處理延伸模組都可以提供自訂功能來支援報表處理。 例如，資料處理延伸模組可支援以下類型的功能：  
  
-   分開管理認證與連接字串  
  
-   支援多重值參數  
  
-   擷取資料來源上所計算的伺服器彙總  
  
-   從資料來源擷取資料屬性及資料值  
  
## 了解資料提供者  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者 (有時稱為驅動程式) 可支援一組標準 <xref:System.Data> 介面來讀取、寫入及更新資料來源上的資料。 當特定類型的資料來源沒有可用的資料處理延伸模組時，可以使用資料提供者。 市面上有許多可用的協力廠商標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者。  
  
 因為 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 具有可延伸的資料提供者架構，所以您可以建置自訂的資料處理延伸模組，以包含 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組所提供的額外功能。 如需詳細資訊，請參閱 [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)。 如需協力廠商資料處理延伸模組的資訊，請參閱協力廠商資料處理延伸模組所隨附的文件。  
  
> [!NOTE]  
>  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者或自訂的資料處理延伸模組必須經過安裝和註冊後，才能用來存取資料來源中的資料。 資料處理延伸模組必須在報表用戶端上安裝及註冊才能撰寫報表，而且必須安裝在報表伺服器上才能檢視發行的報表。 並非所有資料提供者的設計都是在伺服器環境下運作。 如需詳細資訊，請參閱[註冊標準 .NET Framework Data Provider &#40;SSRS&#41;](../../reporting-services/report-data/register-a-standard-net-framework-data-provider-ssrs.md) 和[部署資料處理延伸模組](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)。  
  
## 請參閱＜  
 [資料處理延伸模組概觀](../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  