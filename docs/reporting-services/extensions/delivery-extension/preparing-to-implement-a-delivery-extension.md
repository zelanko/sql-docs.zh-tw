---
title: "準備實作傳遞延伸模組 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- interfaces [Reporting Services]
- delivery extensions [Reporting Services], implementing
ms.assetid: aee1608d-374f-4ad3-bc23-fe07fdaa52b7
caps.latest.revision: "34"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2dda177e4e7ce827c503ca0aedae759eaad8945a
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="preparing-to-implement-a-delivery-extension"></a>準備實作傳遞延伸模組
  在您實作 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組之前，應該定義要實作的介面。 您需要先決定將如何使用傳遞延伸模組、傳遞延伸模組將需要的設定，以及您將需要實作的特定功能以傳遞報表通知。  
  
 每個 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組必須提供下列功能：  
  
-   代表延伸模組與當地語系化延伸模組名稱的 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 介面實作。  
  
-   <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 實作，建立可用以傳遞報表通知給一般使用者的傳遞延伸模組。  
  
-   處理訂閱之特定使用者資料的功能。  
  
 每個傳遞延伸模組都可以增強以包括下列功能：  
  
-   [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 使用者控制項實作，允許使用者使用報表管理員建立使用傳遞延伸模組的報表訂閱。  
  
 下表描述傳遞延伸模組之可用的介面與類別。  
  
|介面或類別|描述|  
|------------------------|-----------------|  
|<xref:Microsoft.ReportingServices.Interfaces.IExtension> 介面|代表 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的擴充功能。|  
|<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 介面|代表 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的傳遞延伸模組。|  
|<xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> 介面|包含傳遞延伸模組所需的報表伺服器的資訊 (例如，可用轉譯延伸模組的清單)。|  
|<xref:Microsoft.ReportingServices.Interfaces.Setting> 類別|表示延伸模組的設定。|  
|<xref:Microsoft.ReportingServices.Interfaces.Notification> 類別|包含傳遞延伸模組用以傳遞報表的訂閱資訊。|  
|<xref:Microsoft.ReportingServices.Interfaces.Report> 類別|代表報表的特定資訊與方法，允許傳遞延伸模組傳遞報表給使用者。|  
|<xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 類別|表示轉譯延伸模組的輸出。 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 物件包含傳遞延伸模組所需的相關聯檔案名稱與類型資訊，這是為了處理轉譯延伸模組所傳回的資料流。|  
|<xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 介面|表示從報表管理員中的使用者，擷取傳遞延伸模組特定訂閱資訊之使用者控制項 (例如，電子郵件地址或是檔案共用的路徑)。|  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [實作傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
