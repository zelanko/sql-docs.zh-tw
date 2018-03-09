---
title: "Reporting Services 例外處理的最佳做法 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: exceptions [Reporting Services], best practices
ms.assetid: 72fecf28-f02e-4338-b50f-0b21f520302d
caps.latest.revision: "34"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e6ae230c7d3e21ad4b5ac19ab791f63db8d51c50
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="best-practices-for-reporting-services-exception-handling"></a>Reporting Services 例外處理的最佳作法
  當開發 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 應用程式時，您可以使用幾個方法來消除或是減少例外狀況的發生次數。 當例外狀況真的發生時，提供明確且精簡的錯誤訊息給使用者，並加入適當的例外狀況處理，以防止應用程式非預期地結束。  
  
 將要求傳送給報表伺服器 Web 服務的應用程式應該執行下列項目：  
  
-   透過盡可能防止無效的要求以避免造成例外狀況。  
  
-   盡可能快取例外狀況並提供特定的錯誤處理程式碼。  
  
-   處理未擲回例外狀況的錯誤案例。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[防止無效的要求](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/preventing-invalid-requests.md)|描述可用以防止將無效的要求傳送到報表伺服器的技術。|  
|[使用 Try 和 Catch 區塊](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md)|描述如何進一步使用 Try/Catch 區塊來增強應用程式的可靠性。|  
|[處理未造成例外狀況的警告與案例](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/handling-warnings-and-cases-that-do-not-cause-exceptions.md)|說明如何處理錯誤才不會造成 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 擲回例外狀況。|  
|[使用 Detail 屬性來處理特定的錯誤](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)|說明如何使用 **SoapException** 物件的 **Detail** 屬性，以程式設計的方式處理特定錯誤。|  
  
## <a name="see-also"></a>另請參閱  
 [Detail 屬性](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Reporting Services 中的例外狀況處理簡介](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
