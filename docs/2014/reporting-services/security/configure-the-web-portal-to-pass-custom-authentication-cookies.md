---
title: 設定報表管理員傳遞自訂驗證 Cookie |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: 17
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 391326882d3eaa0170bee0aa075e9d9b6c15abcb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37266114"
---
# <a name="configure-report-manager-to-pass-custom-authentication-cookies"></a>設定報表管理員傳遞自訂驗證 Cookie
  如果您要使用自訂驗證延伸模組，您應配置報表管理員來傳送自訂驗證 Cookie。 否則，報表管理員只能透過報表伺服器特定的 HTTP 要求來傳送 Cookie。 如果您要傳送其他 Cookie，就必須修改 RSReportServer.Config 檔。  
  
## <a name="modifying-the-rsreportserverconfig-file"></a>修改 RSReportServer.Config 檔  
 您可以啟用報表管理員來加傳送其他 cookie 傳送至報表伺服器 <`PassThroughCookies`> RSReportServer.config 檔案中的報表管理員組態設定的項目。 當單一登入驗證方案不僅需要報表伺服器驗證 Cookie，同時也需要協力廠商驗證系統提供的 Cookie 時，傳送其他 Cookie 這項功能就顯得非常有用。  
  
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
 [設定和管理報表伺服器&#40;SSRS 原生模式&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  
