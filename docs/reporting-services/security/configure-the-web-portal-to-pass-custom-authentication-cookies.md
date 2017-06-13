---
title: "設定入口網站，以傳遞自訂驗證 Cookie |Microsoft 文件"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 0f1131c191fa64c6dc6f2a074a9cd5db7a8b0e1b
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>設定入口網站傳遞自訂驗證 Cookie

如果您使用自訂驗證延伸模組，您應該設定入口網站，才能傳送自訂驗證 cookie。 否則，入口網站只會將傳送透過報表伺服器特有的 HTTP 要求的 cookie。 如果您要傳送其他 Cookie，就必須修改 RSReportServer.Config 檔。

## <a name="modifying-the-rsreportserverconfig-file"></a>修改 RSReportServer.Config 檔

您可以啟用[!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]來傳送其他 cookie 到報表伺服器加入\< **PassThroughCookies**> RSReportServer.config 檔案中的 web 入口網站的組態設定的項目。 當單一登入驗證方案不僅需要報表伺服器驗證 Cookie，同時也需要協力廠商驗證系統提供的 Cookie 時，傳送其他 Cookie 這項功能就顯得非常有用。

若要啟用使用 web 入口網站時，透過 HTTP 要求傳送其他 cookie，請設定下列項目在 RSReportServer.config 檔案中：
  
```  
<UI>  
   <CustomAuthenticationUI>  
      ...  
      <PassThroughCookies>  
         <PassThroughCookie>cookiename1</PassThroughCookie>  
         <PassThroughCookie>cookiename2</PassThroughCookie>  
      </PassThroughCookies>  
   </CustomAuthenticationUI>  
      ...  
</UI>  
```  
  
## <a name="see-also"></a>另請參閱

[使用報表伺服器驗證](../../reporting-services/security/authentication-with-the-report-server.md)   
[RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[安全性延伸模組概觀](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[設定及管理報表伺服器 &#40;SSRS 原生模式 &#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
更多問題嗎？ [再試一次 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
