---
title: "例外狀況處理 Reporting Services 中簡介 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
caps.latest.revision: 29
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ae960b1dd8fc1020b5095e0af920464794905ee2
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="introducing-exception-handling-in-reporting-services"></a>Reporting Services 中的例外狀況處理簡介
  如果您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式將要求傳送到報表伺服器 Web 服務，但是此服務無法處理，則服務會將 SOAP 例外狀況傳回用戶端。 報表伺服器 Web 服務擲回的處理例外狀況是所開發應用程式的重要部分之一，因為當錯誤發生時，可以傳回有用的資訊給使用者。  
  
 本節包含的特定資訊，是有關處理例外狀況以防止使用者的無效輸入，並將有意義的錯誤資訊傳回給使用者。 一般例外狀況處理的詳細資訊，請參閱 < 處理和擲回例外狀況 」，在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文件。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[Reporting Services 中的例外狀況處理](../../reporting-services/report-server-web-service-net-framework-exception-handling/handling-exceptions-in-reporting-services.md)|提供 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的例外狀況概觀以及從 Web 服務傳回錯誤的 SOAP 角色。|  
|[Reporting Services 例外處理的最佳作法](../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/best-practices-for-reporting-services-exception-handling.md)|提供如何處理 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的例外狀況之建議。|  
|[Reporting Services SoapException 類別](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)|描述**SoapException**類別[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和.NET Framework 建置應用程式](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
