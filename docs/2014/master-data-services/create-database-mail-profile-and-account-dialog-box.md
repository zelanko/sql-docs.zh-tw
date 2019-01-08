---
title: 建立 Database Mail 設定檔和帳戶對話方塊 （Master Data Services 組態管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.dbmailprofileacct.f1
ms.assetid: b93ea3d4-9f22-490e-8e26-d766b454aed6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 521afe37ef58a8b2e325bb513c7bdee2a1ed66a2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52760970"
---
# <a name="create-database-mail-profile-and-account-dialog-box-master-data-services-configuration-manager"></a>建立 Database Mail 設定檔和帳戶對話方塊 (Master Data Services 組態管理員)
  使用 [建立 Database Mail 設定檔和帳戶] 對話方塊，即可建立 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的 Database Mail 設定檔和 Database Mail 帳戶。 當商務規則驗證失敗時，將會使用這個設定檔來透過電子郵件通知使用者和群組。  
  
## <a name="database-mail-profile-and-account"></a>Database Mail 設定檔和帳戶  
 「Database Mail 設定檔」是 Database Mail 帳戶的集合。 「Database Mail 帳戶」包含 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用來傳送電子郵件給 SMTP 伺服器的資訊。 當您在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中建立設定檔和帳戶時，此帳戶會自動加入到設定檔，而且將會使用該帳戶資訊來傳送電子郵件。  
  
> [!NOTE]  
>  您無法使用 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 來更新現有的 Database Mail 設定檔或帳戶，也無法為設定檔設定一個以上的帳戶。 若要使用 Database Mail 來執行更進階的工作，您可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 Transact-SQL 指令碼。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的 [Database Mail 組態物件](../relational-databases/database-mail/database-mail-configuration-objects.md) 一節。  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**設定檔名稱**|輸入新 Database Mail 設定檔的名稱。 這個名稱在已設定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的 Database Mail 設定檔中必須是唯一的。<br /><br /> 當您建立這個設定檔之後，就可以在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 的 [資料庫] 頁面上使用及選取此設定檔。|  
|**帳戶名稱**|輸入要與這個設定檔產生關聯的新 Database Mail 帳戶名稱。 這個名稱在已設定 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的 Database Mail 帳戶中必須是唯一的。 這個帳戶並不對應至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 帳戶或 Windows 使用者帳戶。|  
  
## <a name="outgoing-smtp-mail-server"></a>外寄 (SMTP) 郵件伺服器  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**電子郵件地址**|輸入帳戶之電子郵件地址的名稱。 這是寄出電子郵件的電子郵件地址，而且必須使用以下格式： *email_name*@*domain_name*。 範例電子郵件地址為 sales@contoso.com。|  
|**顯示名稱**|選擇性設定。 輸入要在這個帳戶所送出的電子郵件訊息上顯示的名稱。 範例顯示名稱為 Contoso 業務小組。|  
|**回覆電子郵件地址**|選擇性設定。 輸入將用來回覆這個帳戶所送出之電子郵件訊息的電子郵件地址。 範例回覆電子郵件地址為 admin@contoso.com。|  
|**SMTP 伺服器**|輸入帳戶用來傳送電子郵件的 SMTP 伺服器名稱或 IP 位址。 範例 SMTP 伺服器格式為`smtp.` *< 公司名稱 >*`.com`。 如需相關說明，請洽詢您的郵件管理員。|  
|**通訊埠編號**|輸入此帳戶之 SMTP 伺服器的通訊埠編號。 預設 SMTP 通訊埠為 25。|  
|**這個伺服器需要安全連接 (SSL)**|使用安全通訊端層 (SSL) 將通訊加密。|  
  
## <a name="smtp-authentication"></a>SMTP 驗證  
 Database Mail 可以使用 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]的認證、使用您提供的其他認證或以匿名方式傳送。 最佳作法如下：如果電子郵件伺服器需要驗證，請建立要用於 Database Mail 的特定使用者帳戶。 這個使用者帳戶應該具有最小權限，而且不應該為任何其他目的使用。  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**使用 Database Engine 服務認證的 Windows 驗證**|指定 Database Mail 應該使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] Windows 服務帳戶的認證在 SMTP 伺服器上驗證。|  
|**基本驗證**|指定 Database Mail 應該使用特定的使用者名稱和密碼在 SMTP 伺服器上驗證。 此資訊僅用於電子郵件伺服器的驗證，而且帳戶不需要對應到執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之電腦上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用者。|  
|**使用者名稱**|輸入 Database Mail 用來登入 SMTP 伺服器之使用者帳戶的名稱。 如果 SMTP 伺服器需要基本驗證，則使用者名稱是必要的。|  
|**密碼**|輸入 Database Mail 用來登入 SMTP 伺服器的密碼。 如果 SMTP 伺服器需要基本驗證，則需要密碼。|  
|**確認密碼**|再次輸入密碼，以便確認密碼。|  
|**匿名驗證**|指定 SMTP 伺服器不需要驗證。 Database Mail 將不會使用任何認證來進行 SMTP 伺服器驗證。|  
  
## <a name="see-also"></a>另請參閱  
 [資料庫組態頁面 &#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [設定 Master Data Services 的資料庫與網站](set-up-the-database-and-website-for-master-data-services.md)  
  
  
