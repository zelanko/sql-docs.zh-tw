---
title: "報表伺服器 Web 服務 |Microsoft 文件"
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
- SSIS, Web service
- Web service [Reporting Services]
- Reporting Services, extending
- SQL Server Reporting Services, Web service
- Reporting Services, Web service
- XML Web service [Reporting Services]
- Report Server Web service
ms.assetid: 16c21dec-6b46-4497-9a0c-1b0f2b6ab8fc
caps.latest.revision: 47
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 10769f49396bcf32d437e4bee9b04cbc2a3c8d9c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="report-server-web-service"></a>報表伺服器 Web 服務
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]提供存取報表伺服器透過報表伺服器 Web 服務的完整功能。 報表伺服器 Web 服務是一種具有 SOAP API 的 XML Web 服務。 它使用 SOAP over HTTP，並做為用戶端程式與報表伺服器之間的通訊介面。 Web 服務提供兩個端點 (一個用於報表執行，一個用於報表管理)，並含有可公開報表伺服器功能的方法，這些方法可讓您為任何部分的報表生命週期建立自訂工具。  
  
 有三種主要的方式開發[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Web 服務為基礎的應用程式。 您可以：  
  
-   開發應用程式使用[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]和[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK。 如需有關使用[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]建置 Web 服務應用程式，請參閱[建置應用程式使用 Web 服務和.NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)。  
  
-   開發應用程式使用**rs**公用程式 (RS.exe)，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]指令碼環境。 與[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]指令碼，您可以執行任何報表伺服器 Web 服務作業。 如需有關指令碼的[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，請參閱[指令碼會使用 rs.exe 公用程式與 Web 服務](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)。  
  
-   使用任何啟用 SOAP 的開發工具集來開發應用程式。 如需詳細資訊，請參閱[The Role of SOAP in Reporting Services](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md)。  
  
## <a name="programming-diagram"></a>程式設計圖表  
 ![報表伺服器 Web 服務開發選項](../../reporting-services/report-server-web-service/media/reportserviceswebserviceprog-01.gif "報表伺服器 Web 服務開發選項")  
Reporting Services 可用的 Web 服務開發選項  
  
## <a name="in-this-section"></a>本節內容  
 [報表伺服器 Web 服務方法](../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)  
 描述每個報表伺服器 Web 服務的功能及方法。  
  
 [Reporting Services 中 SOAP 的角色](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md)  
 提供 SOAP 的概觀以及在報表伺服器 Web 服務中如何使用它。  
  
 [存取 SOAP API](../../reporting-services/report-server-web-service/accessing-the-soap-api.md)  
 描述 Web 服務描述語言 (WSDL) 並提供 URL 以存取 Reporting Services WSDL 檔案。  
  
 [使用 Web 服務和.NET Framework 建置應用程式](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
 包含有關開發應用程式與 Web 服務以呼叫 Reporting Services SOAP API 的資訊。  
  
 [利用 rs.exe 公用程式和 Web 服務編寫指令碼](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
 提供 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 指令碼環境的概觀。  
  
 [技術參考 &#40;SSRS &#41;](../../reporting-services/technical-reference-ssrs.md)  
 包含報表伺服器 Web 服務方法及對應之複雜類型的特有參考資料。  
  
## <a name="user-requirements-for-web-service-development"></a>Web 服務開發的使用者需求  
 若要使用報表伺服器 Web 服務開發應用程式，您需要：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)]Internet Explorer 5.5 或更新版本的網際網路連線，以及存取報表伺服器的電腦上安裝。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]或[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 安裝在電腦上，如果您想要開發並部署[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]應用程式使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]。  
  
-   深入瞭解[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]特色與功能。  
  
-   對 SOAP 和 [!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)] 有確實的了解。  
  
-   開發經驗[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-相容的語言，例如[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[csprcs](../../includes/csprcs-md.md)]或[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]，如果您打算使用[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]做為您的開發平台。  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器 Web 服務](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
