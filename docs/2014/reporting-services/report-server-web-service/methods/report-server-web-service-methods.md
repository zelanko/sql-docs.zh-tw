---
title: 報表伺服器 Web 服務方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, methods
- Web service [Reporting Services], methods
- XML Web service [Reporting Services], features
- Web service [Reporting Services], features
- Report Server Web service, features
- XML Web service [Reporting Services], methods
ms.assetid: ce5afa27-e90c-44a7-b204-098a065b3665
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 37d0031ebfb4ec6d31da6aad9a8842c0623cb75b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63283474"
---
# <a name="report-server-web-service-methods"></a>報表伺服器 Web 服務方法
  報表伺服器 Web 服務包含數個以元件功能為基礎的方法類別。 這些方法是透過多個 Web 服務端點 (三個用於報表管理，一個用於報表執行) 而提供，這些端點會公開為 <xref:ReportService2010.ReportingService2010> 和 <xref:ReportExecution2005.ReportExecutionService> 類別的成員。 這些類別可透過 wsdl.exe 之類的 Proxy 類別工具產生，此工具包含在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 中。 如需報表伺服器 Web 服務和 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 的詳細資訊，請參閱[使用 Web 服務和 .NET Framework 建置應用程式](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)。  
  
## <a name="endpoints-and-methods"></a>端點和方法  
 下表將列出報表伺服器 Web 服務的端點，以及 <xref:ReportService2010.ReportingService2010> 端點所提供之方法的類別目錄。 如需其他端點所提供之方法的詳細資訊，請參閱[技術參考 &#40;SSRS&#41;](../../technical-reference-ssrs.md)。  
  
|主題|描述|  
|-----------|-----------------|  
|[報表伺服器 Web 服務端點](report-server-web-service-endpoints.md)|描述報表伺服器 Web 服務的管理和執行端點。|  
|[報表伺服器命名空間管理方法](report-server-namespace-management-methods.md)|描述您可以用於管理報表伺服器資料庫的方法。 也就是說，您可以管理資料夾和資源並設定項目屬性。|  
|[授權方法](authorization-methods.md)|描述可用於管理工作、角色和原則的方法。|  
|[資料來源和連線方法](data-sources-and-connection-methods.md)|描述可用於為報表設定資料來源連接及認證資訊並進行管理的方法。|  
|[報表參數方法](report-parameters-methods.md)|描述可用於為報表設定及擷取參數的方法。|  
|[模型方法](../report-server-web-service.md)|描述可用於管理模型的方法。|  
|[轉譯及執行方法](rendering-and-execution-methods.md)|描述可用於管理報表執行、轉譯和快取的方法。|  
|[報表記錄方法](report-history-methods.md)|描述可用於建立並管理報表記錄快照的方法。|  
|[排程方法](scheduling-methods.md)|描述可用於建立並管理報表伺服器所使用之共用排程和快取重新整理計劃的方法。|  
|[訂閱與傳遞方法](subscription-and-delivery-methods.md)|描述可用於建立並管理訂閱和報表傳遞的方法。|  
|[連結報表方法](linked-reports-methods.md)|描述可用於建立並管理連結報表的方法。|  
  
## <a name="see-also"></a>另請參閱  
 [存取 SOAP API](../accessing-the-soap-api.md)   
 [使用 Web 服務和 .NET Framework 建置應用程式](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [報表伺服器 Web 服務](../report-server-web-service.md)   
 [技術參考 &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
