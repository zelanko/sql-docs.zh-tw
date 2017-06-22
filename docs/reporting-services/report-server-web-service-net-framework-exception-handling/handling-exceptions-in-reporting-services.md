---
title: "Reporting Services 中處理例外狀況 |Microsoft 文件"
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
- SOAP [Reporting Services], exceptions
- .NET Framework [Reporting Services]
- exceptions [Reporting Services], about exception handling
- SoapException object
ms.assetid: 1a443432-2db5-48c5-bc29-433b4688082f
caps.latest.revision: 31
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1cf3ca01075260274b363736bd53c245809e521c
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="handling-exceptions-in-reporting-services"></a>處理 Reporting Services 中的例外狀況
  無法完成 Reporting Services SOAP API 用戶端要求時，報表伺服器會傳回錯誤，而非呼叫的預期結果。 無法完成呼叫，會傳回錯誤，而報表伺服器 Web 服務 SOAP 做**錯誤**XML 項目。 索引鍵錯誤的描述性項目，則**詳細**元素，其包含所有報表伺服器，以及任何其他 Web 服務錯誤資訊所提供的錯誤資訊。 中的索引鍵資訊**詳細**項目是報表伺服器錯誤碼。 您可以根據訊息與錯誤碼，決定要在應用程式中採取的下一個適當動作。 如需有關 SOAP 錯誤的詳細資訊，請參閱全球資訊網協會 (W3C) 網站，網址為 http://www.w3.org/TR/SOAP。  
  
## <a name="soap-faults-and-the-net-framework"></a>SOAP 錯誤與 .NET Framework  
 在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]，如果 Web 服務用戶端要求中發生錯誤，報表伺服器進行通訊之用戶端程式碼可呼叫此 Web 服務擲回錯誤**SoapException**物件。 **SoapException**包裝 SOAP 錯誤中包含的資訊。 **詳細**屬性**SoapException**對應至**詳細**SOAP 錯誤中的項目。 應用程式應該攔截**SoapException**物件使用 try/catch 區塊，並使用**詳細**屬性**SoapException**採取適當動作。 如需有關**SoapException**類別和**詳細**屬性[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，請參閱[Reporting Services SoapException 類別](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)。 如需有關**SoapException**類別，請參閱[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 文件。  
  
## <a name="see-also"></a>另請參閱  
 [Detail 屬性](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [例外狀況處理中的 Reporting Services 簡介](../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
