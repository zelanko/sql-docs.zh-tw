---
title: 通知 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- notifications [Master Data Services]
- notifications [Master Data Services], about notifications
- e-mail [Master Data Services]
- e-mail [Master Data Services], about e-mail notifications
ms.assetid: d7ad32d5-9fe5-48fd-8c61-0b00c0aff082
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 7b973d967645b51aafe7e4314b339c5966fa7141
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47671586"
---
# <a name="notifications-master-data-services"></a>通知 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 可設定為在商務規則驗證失敗、模型版本狀態變更或變更集狀態變更時，傳送電子郵件通知。  
  
## <a name="how-notifications-are-sent"></a>通知的傳送方式  
 您在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中設定通知。 通知會在主控 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 執行個體上，利用 Database Mail 傳送電子郵件訊息。 如需詳細資訊，請參閱《 [線上叢書》中的](../relational-databases/database-mail/database-mail-configuration-objects.md) Database Mail 組態物件 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。  
  
## <a name="when-notifications-are-sent"></a>通知的傳送時間  
 設定通知之後，在下列情況下會自動傳送電子郵件通知。  
  
|執行個體|Description|  
|--------------|-----------------|  
|資料的商務規則驗證失敗|個別商務規則必須設定為屬性值的商務規則驗證失敗時傳送電子郵件。 通知包含下列資訊。<br /><br /> [模型]<br /><br /> Version<br /><br /> 實體<br /><br /> 成員代碼<br /><br /> 失敗的商務規則<br /><br /> 屬性值未通過商務規則的成員連結<br /><br /> 發出通知的時間<br /><br /> 如需詳細資訊，請參閱 [設定商務規則來傳送通知 &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)中設定通知。|  
|模型版本狀態變更|每次模型版本的狀態變更時，身為模型管理員的使用者會自動接收通知。 通知包含下列資訊。<br /><br /> [模型]<br /><br /> Version<br /><br /> 版本的先前狀態與新狀態<br /><br /> 發出通知的時間<br /><br /> 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。|  
|變更集的狀態變更|每當變更集狀態為需要核准的實體進行變更時，實體管理員及 (或) 變更集擁有者就會自動收到通知。 通知包含下列資訊。<br /><br /> [模型]<br /><br /> Version<br /><br /> 變更集名稱<br /><br /> 先前狀態<br /><br /> 新狀態<br /><br /> 套用變更集以檢視和修改暫止變更的連結。<br /><br /> 如需詳細資訊，請參閱[變更集 &#40;Master Data Services&#41;](../master-data-services/changesets-master-data-services.md)|  
  
## <a name="system-settings"></a>系統設定  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中有一些設定會影響通知。 您可以在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中或直接在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫 [系統設定] 資料表中調整這些設定。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|設定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 傳送電子郵件通知。|[設定電子郵件通知 &#40;Master Data Services&#41;](../master-data-services/configure-email-notifications-master-data-services.md)|  
|設定 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 在屬性值變更時傳送通知。|[設定商務規則來傳送通知 &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [商務規則 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
-   [版本 &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)  
  
-   [疑難排解電子郵件通知 (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)  
  
  
