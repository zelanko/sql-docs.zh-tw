---
title: "設定報表管理員傳遞自訂驗證 Cookie | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "驗證 [Reporting Services]"
  - "延伸模組 [Reporting Services], 自訂安全性"
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 18
---
# 設定報表管理員傳遞自訂驗證 Cookie
  如果您要使用自訂驗證延伸模組，您應配置 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 來傳送自訂驗證 Cookie。 否則，[!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 只能透過報表伺服器特定的 HTTP 要求來傳送 Cookie。 如果您要傳送其他 Cookie，就必須修改 RSReportServer.Config 檔。  
  
## 修改 RSReportServer.Config 檔  
 您可以將 \<**PassThroughCookies**> 元素加入至 RSReportServer.config 檔中的 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 組態設定，藉以讓 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 將其他 Cookie 傳送至報表伺服器。 當單一登入驗證方案不僅需要報表伺服器驗證 Cookie，同時也需要協力廠商驗證系統提供的 Cookie 時，傳送其他 Cookie 這項功能就顯得非常有用。  
  
 使用 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 時，若要能夠透過 HTTP 要求來傳送其他 Cookie，則必須在 RSReportServer.config 檔中設定下列元素：  
  
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
  
## 另請參閱  
 [使用報表伺服器驗證](../../reporting-services/security/authentication-with-the-report-server.md)   
 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [安全性延伸模組概觀](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
 [設定和管理報表伺服器 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  