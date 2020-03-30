---
title: 呼叫 Web 服務方法 | Microsoft Docs
description: 呼叫 Proxy 類別的方法，以在報表伺服器上執行報表作業。 Web 服務方法具有公用存取權，且需要適當的引數。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- Web service [Reporting Services], calls
- calling Web service
- Report Server Web service, SOAP
- XML Web service [Reporting Services], calls
- Report Server Web service, calls
- XML Web service [Reporting Services], SOAP
- SOAP [Reporting Services], calls
ms.assetid: f6f0c6e3-8bb5-4c44-9d19-1872edc72746
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0e7347bfcb93d327bc6e56eb91c903bbc5e1f38f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "79198323"
---
# <a name="calling-web-service-methods"></a>呼叫 Web 服務方法
  當您使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Proxy 類別來呼叫 Web 服務作業時，可以使用該類別的方法來這樣做。 這些方法會像在 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 類別庫中類別的任何其他方法一樣回應。 所有的 Web 服務方法都有公用存取權，而且會要求您提供適當數目的引數與引數類型。 在專案中建立 Proxy 類別的執行個體之後，可以呼叫方法來透過報表伺服器執行報表作業。 下列 C# 程式碼範例說明 <xref:ReportService2010.ReportingService2010.ListChildren%2A> Proxy 類別的 <xref:ReportService2010.ReportingService2010> 方法。 此程式碼是用以遞迴呼叫傳回 <xref:ReportService2010.CatalogItem> 物件陣列的 Web 服務，這些物件包含報表伺服器資料庫中所有項目的清單：  
  
```vb  
Dim rs As New ReportingService2010()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
Dim items As CatalogItem() = rs.ListChildren("/", True)  
```  
  
```csharp  
ReportingService2010 rs = new ReportingService2010();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
CatalogItem[] items = rs.ListChildren("/", true);  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [報表伺服器 Web 服務](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [技術參考 &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
