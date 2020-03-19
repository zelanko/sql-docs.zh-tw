---
title: 報表伺服器 Web 服務 | Microsoft Docs
description: Reporting Services 提供報表伺服器與報表伺服器 Web 服務 (用於報表執行和管理的 SOAP 服務端點) 的功能。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- SSIS, Web service
- Web service [Reporting Services]
- Reporting Services, extending
- SQL Server Reporting Services, Web service
- Reporting Services, Web service
- XML Web service [Reporting Services]
- Report Server Web service
ms.assetid: 16c21dec-6b46-4497-9a0c-1b0f2b6ab8fc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6fb059d867a7a3448e5a842929df48ad009f2518
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/12/2020
ms.locfileid: "79198475"
---
# <a name="report-server-web-service"></a>報表伺服器 Web 服務
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 透過報表伺服器 Web 服務提供報表伺服器的完整功能。 報表伺服器 Web 服務是一種具有 SOAP API 的 XML Web 服務。 它使用 SOAP over HTTP，並做為用戶端程式與報表伺服器之間的通訊介面。 Web 服務提供兩個端點 (一個用於報表執行，一個用於報表管理)，並含有可公開報表伺服器功能的方法，這些方法可讓您為任何部分的報表生命週期建立自訂工具。  
  
 有三種主要的方式可開發以 Web 服務為基礎的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式。 您可以：  
  
-   使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 來開發應用程式。 如需使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 建置 Web 服務應用程式的詳細資訊，請參閱[使用 Web 服務和 .NET Framework 建置應用程式](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)。  
  
-   使用 **rs** 公用程式 (RS.exe)，即 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 指令碼環境來開發應用程式。 透過 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 與 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 指令碼，您可以執行任何報表伺服器 Web 服務作業。 如需以 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 編寫指令碼的詳細資訊，請參閱[利用 rs.exe 公用程式與 Web 服務編寫指令碼](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)。  
  
-   使用任何啟用 SOAP 的開發工具集來開發應用程式。 如需詳細資訊，請參閱 [Reporting Services 中的 SOAP 角色](../../reporting-services/report-server-web-service/the-role-of-soap-in-reporting-services.md)。  
  
## <a name="programming-diagram"></a>程式設計圖表  
 ![報表伺服器 Web 服務部署選項](../../reporting-services/report-server-web-service/media/reportserviceswebserviceprog-01.gif "報表伺服器 Web 服務部署選項")  
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
  
 [利用 rs.exe 公用程式與 Web 服務編寫指令碼](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
 提供 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 指令碼環境的概觀。  
  
 [技術參考 &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
 包含報表伺服器 Web 服務方法及對應之複雜類型的特有參考資料。  
  
## <a name="user-requirements-for-web-service-development"></a>Web 服務開發的使用者需求  
 若要使用報表伺服器 Web 服務開發應用程式，您需要：  
  
-   在有網際網路連線及可存取報表伺服器的電腦上安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 5.5 或更新的版本。  
  
-   如果您想要使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 來開發和部署 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 應用程式，則需要在電腦上安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK。  
  
-   對 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的特性與功能有深入的了解。  
  
-   對 SOAP 和 [!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)]有確實的了解。  
  
-   如果您計畫使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 作為開發平台，則需要有使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 等 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 相容語言的開發體驗。  
  
## <a name="see-also"></a>另請參閱  
 [報表伺服器 Web 服務](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
