---
title: 設定入口網站傳遞自訂驗證 Cookie | Microsoft Docs
ms.date: 04/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b538523839be0260eda33934a18e682579aaa3f9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810216"
---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>設定入口網站傳遞自訂驗證 Cookie

如果您要使用自訂驗證延伸模組，您應該設定入口網站來傳送自訂驗證 Cookie。 否則，入口網站只能透過報表伺服器特定的 HTTP 要求來傳送 Cookie。 如果您要傳送其他 Cookie，就必須修改 RSReportServer.Config 檔。

## <a name="modifying-the-rsreportserverconfig-file"></a>修改 RSReportServer.Config 檔

您可以將 \<**PassThroughCookies**> 項目新增至 RSReportServer.config 檔中的入口網站組態設定，藉以讓 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 將其他 Cookie 傳送至報表伺服器。 當單一登入驗證方案不僅需要報表伺服器驗證 Cookie，同時也需要協力廠商驗證系統提供的 Cookie 時，傳送其他 Cookie 這項功能就顯得非常有用。

使用入口網站時，若要能夠透過 HTTP 要求來傳送其他 Cookie，則必須在 RSReportServer.config 檔中設定下列項目：
  
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
[設定和管理報表伺服器 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
更多問題嗎？ [試試 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
