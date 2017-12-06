---
title: "處理 Reporting Services 中的例外狀況 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- SOAP [Reporting Services], exceptions
- .NET Framework [Reporting Services]
- exceptions [Reporting Services], about exception handling
- SoapException object
ms.assetid: 1a443432-2db5-48c5-bc29-433b4688082f
caps.latest.revision: "31"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: df0558ddbb66f0a5ff8631464e511d35b94ebec7
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="handling-exceptions-in-reporting-services"></a>處理 Reporting Services 中的例外狀況
  無法完成 Reporting Services SOAP API 用戶端要求時，報表伺服器會傳回錯誤，而非呼叫的預期結果。 無法完成呼叫時，則會以 SOAP **Fault** XML 項目傳回報表伺服器 Web 服務的錯誤。 該錯誤的關鍵描述項目為 **detail** 項目，此項目會包含報表伺服器提供的所有錯誤資訊以及任何其他 Web 服務錯誤資訊。 報表伺服器錯誤碼是 **detail** 項目中的主要資訊。 您可以根據訊息與錯誤碼，決定要在應用程式中採取的下一個適當動作。 如需有關 SOAP 錯誤的詳細資訊，請參閱全球資訊網協會 (W3C) 網站，網址為 http://www.w3.org/TR/SOAP。  
  
## <a name="soap-faults-and-the-net-framework"></a>SOAP 錯誤與 .NET Framework  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中，如果對 Web 服務的用戶端要求中發生錯誤，報表伺服器就會擲回 **SoapException** 物件，來向呼叫 Web 服務的用戶端程式碼通訊該錯誤。 **SoapException** 會包裝 SOAP 錯誤中包含的資訊。 **SoapException** 的 **Detail** 屬性會與 SOAP 錯誤中的 **detail** 項目對應。 應用程式應該使用 try/catch 區塊來捕捉 **SoapException** 物件，並使用 **SoapException** 的 **Detail** 屬性來採取適當的動作。 如需 **SoapException** 類別以及 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中 **Detail** 屬性的詳細資訊，請參閱 [Reporting Services SoapException 類別](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)。 如需 **SoapException** 類別的詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文件。  
  
## <a name="see-also"></a>另請參閱  
 [Detail 屬性](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Reporting Services 中的例外狀況處理簡介](../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
