---
title: 設定電子郵件通知 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- e-mail [Master Data Services], configuring
- notifications [Master Data Services], configuring notifications
ms.assetid: 4241a6ab-7465-471b-9890-57c6b572037e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 658611f42b7b82d653b2af8cc61c6bfa533ac5d4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198028"
---
# <a name="configure-email-notifications-master-data-services"></a>設定電子郵件通知 (Master Data Services)
  當您想要 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 自動傳送電子郵件訊息時，請設定通知電子郵件。  
  
### <a name="to-configure-notifications"></a>設定通知  
  
1.  在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中的 **[資料庫]** 頁面上，選取您的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。  
  
2.  在 **[系統設定]** 區段中，按一下 **[建立設定檔]**。  
  
3.  完成所有必要的欄位。 如需詳細資訊，請參閱[建立 Database Mail 設定檔和帳戶對話方塊 &#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/create-database-mail-profile-and-account-dialog-box.md)。  
  
4.  按一下 [確定] 。  
  
    > [!NOTE]  
    >  當您設定通知之後，就無法使用 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 進行變更。 您必須直接在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中進行變更。 如需詳細資訊，請參閱 [Database Mail Configuration Objects](../relational-databases/database-mail/database-mail-configuration-objects.md)。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中有一些設定會影響通知。 您可以在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中或直接在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫 [系統設定] 資料表中調整這些設定。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](system-settings-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [通知&#40;Master Data Services&#41;](../../2014/master-data-services/notifications-master-data-services.md)   
 [Troubleshooting Email Notifications (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx) (針對電子郵件通知進行疑難排解 (Master Data Services))   
 [設定商務規則來傳送通知&#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
