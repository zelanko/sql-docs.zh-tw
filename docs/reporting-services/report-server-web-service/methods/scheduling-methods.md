---
title: "排程方法 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- schedules [Reporting Services], methods
- reports [Reporting Services], scheduling
- shared schedules [Reporting Services], methods
- methods [Reporting Services], scheduling
ms.assetid: 68ae13f9-d91e-4572-a82a-8fa42001569e
caps.latest.revision: 35
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3c7360e28e7dd59f258fd43aa0440866528b9e32
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="scheduling-methods"></a>排程方法
  您可以使用這些方法來建立並管理執行和傳遞報表的共用排程，並快取報表伺服器所運用的重新整理計劃。  
  
|方法|動作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateCacheRefreshPlan%2A>|建立項目的快取重新整理計劃。|  
|<xref:ReportService2010.ReportingService2010.CreateSchedule%2A>|建立新的共用排程。|  
|<xref:ReportService2010.ReportingService2010.DeleteCacheRefreshPlan%2A>|刪除快取重新整理計劃。|  
|<xref:ReportService2010.ReportingService2010.DeleteSchedule%2A>|刪除根據特定排程識別碼的共用排程。|  
|<xref:ReportService2010.ReportingService2010.GetCacheRefreshPlanProperties%2A>|傳回指定之快取重新整理計劃的屬性。|  
|<xref:ReportService2010.ReportingService2010.GetScheduleProperties%2A>|傳回共用排程的屬性值。|  
|<xref:ReportService2010.ReportingService2010.ListCacheRefreshPlans%2A>|傳回與目錄項目關聯的快取重新整理計劃清單。|  
|<xref:ReportService2010.ReportingService2010.ListScheduledItems%2A>|傳回與共用排程關聯的項目清單。|  
|<xref:ReportService2010.ReportingService2010.ListSchedules%2A>|傳回報表伺服器或 SharePoint 網站上所有共用排程的清單。|  
|<xref:ReportService2010.ReportingService2010.ListScheduleStates%2A>|傳回支援的排程狀態清單。|  
|<xref:ReportService2010.ReportingService2010.PauseSchedule%2A>|暫停給定排程的執行。|  
|<xref:ReportService2010.ReportingService2010.ResumeSchedule%2A>|繼續已暫停的共用排程。|  
|<xref:ReportService2010.ReportingService2010.SetCacheRefreshPlanProperties%2A>|設定快取重新整理計劃的屬性。|  
|<xref:ReportService2010.ReportingService2010.SetScheduleProperties%2A>|設定共用排程的屬性值。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和.NET Framework 建置應用程式](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [報表伺服器 Web 服務](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [報表伺服器 Web 服務方法](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [技術參考 &#40;SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
