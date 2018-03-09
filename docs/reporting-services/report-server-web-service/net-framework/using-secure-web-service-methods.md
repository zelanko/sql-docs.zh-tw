---
title: "使用安全的 Web 服務方法 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- SOAP [Reporting Services], secure connections
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: 87329299-c2ea-4517-9148-d855726768a9
caps.latest.revision: "36"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9640abf1d603ebc5acb62026df20e9d3cdd3bd81
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="using-secure-web-service-methods"></a>使用安全的 Web 服務方法
  某些報表伺服器 Web 服務方法在叫用時，可能需要安全的連接。 需要安全連線的方法是由 RSReportServer.config 檔案中的 **SecureConnectionLevel** 設定所決定。 設定值有效範圍為 0 及以上的整數值。 下表描述這些值。  
  
|層級|描述|  
|-----------|-----------------|  
|**0**|不安全。 對 Reporting Services SOAP API 的呼叫不需要安全連接。|  
|大於 **0**|安全。 所有對 Reporting Services SOAP API 的呼叫都需要安全連接。|  
  
 您可以使用 Web 服務的 <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> 方法，根據報表伺服器目前的組態，傳回需要安全連接的 Web 服務方法清單。 在 SSL 案例中，您應該評估 <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> 傳回的方法清單，並視要呼叫的方法而定，將 Web 服務的配置名稱變更為 "https" 或 "http"。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [報表伺服器 Web 服務](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
