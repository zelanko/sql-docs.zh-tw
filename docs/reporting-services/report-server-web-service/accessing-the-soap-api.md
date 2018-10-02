---
title: 存取 SOAP API | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- XML Web service [Reporting Services], WSDL
- Web service [Reporting Services], SOAP
- calling Web service
- SOAP [Reporting Services], accessing
- Report Server Web service, SOAP
- Web service [Reporting Services], WSDL
- WSDL [Reporting Services]
- XML Web service [Reporting Services], SOAP
- Report Server Web service, WSDL
- referencing WSDL
ms.assetid: 63bb870a-4dbf-46bd-8921-78f8ebe5fd75
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bf21f49e7160c641404122fa36a104d6d49f0e42
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758526"
---
# <a name="accessing-the-soap-api"></a>存取 SOAP API
  報表伺服器 Web 服務透過 HTTP 使用簡易物件存取通訊協定 (SOAP)，並在用戶端程式與報表伺服器之間當做通訊介面。 Web 服務提供兩個端點 (一個用於報表執行，一個用於報表管理)，並且含有方法以及一組您可用以存取完整功能的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之複雜類型的物件。 若要呼叫服務，您必須參考 Reporting Services Web 服務描述語言 (WSDL)。  
  
## <a name="referencing-the-reporting-services-wsdl"></a>參考 Reporting Services WSDL  
 若要順利呼叫 Web 服務，您必須知道如何存取服務，服務支援哪些作業、服務需要哪些參數以及服務會傳回哪些內容。 WSDL 是以電腦可讀取或處理的 XML 文件提供這項資訊。  
  
 報表伺服器 Web 服務是以三個不同的端點公開。 每個端點都有不同的 WSDL 檔案名稱。 <xref:ReportService2010> 端點包含以原生模式或 SharePoint 整合模式在報表伺服器上管理物件的方法。 這個端點的 WSDL 是透過 `ReportService2010.asmx?wsdl.` 來存取。  
  
> [!NOTE]  
>  <xref:ReportService2005> 和 <xref:ReportService2006> 端點是在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 中被取代。 <xref:ReportService2010> 端點包含這兩個端點的功能，並包含額外的管理功能。  
  
-   <xref:ReportExecution2005> 端點可讓開發人員以程式設計方式處理及轉譯報表伺服器中的報表。 這個端點的 WSDL 是透過 `ReportExecution2005.asmx?wsdl` 來存取。  
  
 WSDL 可由支援 SOAP 與 Web 服務的開發套件所取用，例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK。  
  
 下列範例示範 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 管理 WSDL 檔案的 URL 格式。  
  
```  
http://server/reportserver/ReportService2010.asmx?wsdl  
```  
  
 下表將描述 URL 中的每個元素。  
  
|URL 元素|Description|  
|-----------------|-----------------|  
|*伺服器*|這是部署報表伺服器的伺服器名稱。|  
|*reportserver*|包含 XML Web 服務的資料夾。 這是在安裝期間設定的。|  
|*\<端點名稱>.asmx*|Web 服務端點的名稱。|  
  
 如需有關 WSDL 格式的詳細資訊，請參閱全球資訊網協會 (W3C) WSDL 規格，網址為 http://www.w3.org/TR/wsdl。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [報表伺服器 Web 服務](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
