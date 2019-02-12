---
title: 設定報表管理員傳遞自訂驗證 Cookie |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 6787ec73d91b32e0bdb90f8a5f25499f0ac35620
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034487"
---
# <a name="configure-report-manager-to-pass-custom-authentication-cookies"></a>設定報表管理員傳遞自訂驗證 Cookie
  如果您要使用自訂驗證延伸模組，您應配置報表管理員來傳送自訂驗證 Cookie。 否則，報表管理員只能透過報表伺服器特定的 HTTP 要求來傳送 Cookie。 如果您要傳送其他 Cookie，就必須修改 RSReportServer.Config 檔。  
  
## <a name="modifying-the-rsreportserverconfig-file"></a>修改 RSReportServer.Config 檔  
 您可以將 <`PassThroughCookies`> 元素加入至 RSReportServer.config 檔中的報表管理員組態設定，藉以讓報表管理員將其他 Cookie 傳送至報表伺服器。 當單一登入驗證方案不僅需要報表伺服器驗證 Cookie，同時也需要協力廠商驗證系統提供的 Cookie 時，傳送其他 Cookie 這項功能就顯得非常有用。  
  
 使用報表管理員時，若要能夠透過 HTTP 要求來傳送其他 Cookie，則必須在 RSReportServer.config 檔中設定下列元素：  
  
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
 [使用報表伺服器驗證](authentication-with-the-report-server.md)   
 [RSReportServer 組態檔](../report-server/rsreportserver-config-configuration-file.md)   
 [安全性延伸模組概觀](../extensions/security-extension/security-extensions-overview.md)   
 [設定和管理報表伺服器 &#40;SSRS 原生模式&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  
