---
title: 通知 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- notifications [Master Data Services]
- notifications [Master Data Services], about notifications
- e-mail [Master Data Services]
- e-mail [Master Data Services], about e-mail notifications
ms.assetid: d7ad32d5-9fe5-48fd-8c61-0b00c0aff082
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8213976a69f360fe13fa9d085919992e3daadf4b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023362"
---
# <a name="notifications-master-data-services"></a>通知 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 可以設定要傳送的電子郵件通知，當商務規則驗證失敗或模型版本狀態變更。  
  
## <a name="how-notifications-are-sent"></a>通知的傳送方式  
 您在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中設定通知。 通知會在主控 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 執行個體上，利用 Database Mail 傳送電子郵件訊息。 如需詳細資訊，請參閱《 [線上叢書》中的](../relational-databases/database-mail/database-mail-configuration-objects.md) Database Mail 組態物件 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。  
  
## <a name="when-notifications-are-sent"></a>通知的傳送時間  
 設定通知之後，在下列情況下會自動傳送電子郵件通知。  
  
|執行個體|描述|  
|--------------|-----------------|  
|資料的商務規則驗證失敗|個別商務規則必須設定為屬性值的商務規則驗證失敗時傳送電子郵件。 如需詳細資訊，請參閱[設定商務規則來傳送通知 &#40;Master Data Services&#41;](configure-business-rules-to-send-notifications-master-data-services.md)。|  
|模型版本狀態變更|每次模型版本的狀態變更時，身為模型管理員的使用者會自動接收通知。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。|  
  
## <a name="system-settings"></a>系統設定  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中有一些設定會影響通知。 您可以在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中或直接在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫 [系統設定] 資料表中調整這些設定。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|設定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 傳送電子郵件通知。|[設定電子郵件通知&#40;Master Data Services&#41;](../../2014/master-data-services/configure-email-notifications-master-data-services.md)|  
|設定 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 在屬性值變更時傳送通知。|[設定商務規則來傳送通知&#40;Master Data Services&#41;](configure-business-rules-to-send-notifications-master-data-services.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [商務規則&#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [版本&#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
-   [疑難排解電子郵件通知 (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)  
  
  