---
title: "使用 Reporting Services SOAP 標頭 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-soap-headers
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- SOAP headers [Reporting Services]
- SOAP [Reporting Services], headers
- XML Web service [Reporting Services], SOAP
ms.assetid: 306d2c06-a25a-40f8-8a35-13dd32e8841e
caps.latest.revision: "39"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a3aca058733efe1a4d211065683082117cdc8c65
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="using-reporting-services-soap-headers"></a>使用 Reporting Services SOAP 標頭
  使用 SOAP 與 Web 服務方法通訊需要遵循標準格式。 這個格式的一部分是編碼於 XML 文件中的資料。 XML 文件是由根 **Envelope** 項目所組成，該項目則是由必要的 **Body** 項目和選擇性的 **Header** 項目組成。 **Body** 項目包含訊息特定的資料。 選擇性的 **Header** 項目可能包含其他與特定訊息沒有直接關聯的資訊。 **Header** 項目的每個子項目都稱為 SOAP 標頭。  
  
 雖然 SOAP 標頭可能會包含與訊息相關的資料，但通常是包含由 Web 伺服器基礎結構所處理的資訊。  
  
 報表伺服器 Web 服務定義了多個用於 SOAP 標頭的類別：<xref:ReportService2005.BatchHeader>、<xref:ReportService2010.ItemNamespaceHeader>、<xref:ReportService2010.ServerInfoHeader>、<xref:ReportService2010.TrustedUserHeader> 和 <xref:ReportExecution2005.ExecutionHeader>。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[批次方法](../../reporting-services/report-server-web-service-net-framework-soap-headers/batching-methods.md)|描述如何使用 <xref:ReportService2005.BatchHeader>，在單一交易中批次處理多項作業。|  
|[識別執行狀態](../../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)|描述如何在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，使用 **SessionHeader** 管理工作階段狀態。|  
|[設定 GetProperties 方法的項目命名空間](../../reporting-services/report-server-web-service-net-framework-soap-headers/setting-the-item-namespace-for-the-getproperties-method.md)|描述如何使用 <xref:ReportService2010.ReportingService2010.GetProperties%2A> 方法和 <xref:ReportService2010.ItemNamespaceHeader> SOAP 標頭，根據項目的路徑或識別碼來擷取屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [技術參考 &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
