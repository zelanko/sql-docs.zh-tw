---
title: 建立資料庫精靈 (Master Data Services 組態管理員) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.createdbwiz.f1
ms.assetid: 45fe7a23-a46c-4d40-8bca-3431fbfc5c9d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7207cd8e3a087ed0aa85931254754d4009d73c53
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479874"
---
# <a name="create-database-wizard-master-data-services-configuration-manager"></a>建立資料庫精靈 (Master Data Services 組態管理員)
  使用 [建立資料庫精靈] 可建立 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。  
  
## <a name="database-server"></a>資料庫伺服器  
 指定資訊來連接本機或遠端 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 執行個體，以主控 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫。 若要連接到遠端執行個體，它必須先啟用遠端連接。  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**SQL Server 執行個體**|指定您想要主控 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 資料庫的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 執行個體名稱。 這可以是本機或遠端電腦上的預設或具名執行個體。 輸入以下項目來指定資訊：<br /><br /> 句點 (.)，可連接到您本機電腦上的預設執行個體。<br /><br /> 伺服器名稱或 IP 位址，可連接到指定之本機或遠端電腦上的預設執行個體。<br /><br /> 伺服器名稱或 IP 位址，以及連接到指定之本機或遠端電腦上具名執行個體的執行個體名稱。 使用以下格式指定這項資訊： *server_name*\\*instance_name*。|  
|**驗證類型**|選取連接到指定的 SQL Server 執行個體時所要使用的驗證類型。 您用來連接的認證必須屬於指定之 **執行個體的** 系統管理員 (sysadmin) [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 伺服器角色。 如需系統管理員角色的詳細資訊，請參閱 [伺服器層級角色](../relational-databases/security/authentication-access/server-level-roles.md)。 驗證類型包括：<br /><br /> **目前使用者 - 整合式安全性**：使用 [整合式 Windows 驗證]，透過目前 Windows 使用者帳戶的認證來連線。 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 會使用登入電腦及開啟應用程式之使用者的 Windows 認證。 您不能在應用程式中指定不同的 Windows 認證。 如果您想要使用不同的 Windows 認證來連接，您必須以該使用者的身分登入電腦，然後開啟 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]。<br /><br /> **SQL Server 帳戶**：使用 SQL Server 帳戶來連線。 當您選取這個選項時，將會啟用 [使用者名稱] 和 [密碼] 欄位，而且您必須為指定之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 帳戶指定認證。|  
|**使用者名稱**|指定將要用來連接指定之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的使用者帳戶名稱。 此帳戶必須屬於指定之 **執行個體上的** 系統管理員 (sysadmin) [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 角色。<br /><br /> 當 [驗證類型] 為 [目前使用者 - 整合式安全性]，[使用者名稱] 方塊會是唯讀的，而且它會顯示登入電腦的 Windows 使用者帳戶名稱。<br /><br /> [驗證類型] 為 [SQL Server 帳戶] 時，將會啟用 [使用者名稱] 方塊，而且您必須針對指定之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 帳戶指定認證。|  
|**密碼**|指定與使用者帳戶有關聯的密碼。<br /><br /> 當 [驗證類型] 為 [目前使用者 - 整合式安全性]，[密碼] 方塊會是唯讀的，而且將會使用指定的 Windows 使用者帳戶認證來連接。<br /><br /> [驗證類型] 為 [SQL Server 帳戶] 時，將會啟用 [密碼] 方塊，而且您必須指定與指定的使用者帳戶有關聯的密碼。|  
|**測試連接**|確認指定的使用者帳戶可以連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，而且此帳戶擁有建立該執行個體之 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的權限。 如果您沒有按一下 [測試連接]，則按 [下一步] 時將會測試連接。|  
  
## <a name="database"></a>[資料庫]  
 為新的資料庫指定資料庫名稱和定序選項。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的定序會提供資料的排序規則、大小寫和區分腔調字屬性。 與字元資料類型 (例如 char 和 varchar) 搭配使用的定序會指示字碼頁，以及可針對該資料類型表示的對應字元。 如需資料庫定序的詳細資訊，請參閱 [定序和 Unicode 支援](../relational-databases/collations/collation-and-unicode-support.md)。  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**資料庫名稱**|為 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫指定名稱。|  
|**SQL Server 預設定序**|選取此選項可針對新的資料庫使用指定之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的目前資料庫定序設定。|  
|**Windows 定序**|為新的資料庫指定要使用的 Windows 定序設定。 Windows 定序會依據相關聯的 Windows 地區設定來定義儲存字元資料的規則。 如需 Windows 定序和關聯選項的詳細資訊，請參閱 [Windows 定序名稱 &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)。<br /><br /> 注意:只有當您清除 [SQL Server 預設定序] 方塊之後，[Windows 定序] 清單和關聯的選項才會啟用。|  
  
## <a name="administrator-account"></a>系統管理員帳戶  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**使用者名稱**|指定要成為 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 系統管理員的網域使用者帳戶。 所有[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]與此資料庫，此使用者相關聯的 Web 應用程式可以更新所有模型和所有功能區域中的所有資料。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。|  
  
## <a name="summary"></a>總結  
 顯示選取之選項的摘要。 檢閱您的選擇，然後按一下 [下一步]，開始使用指定的設定建立資料庫。  
  
## <a name="progress-and-finish"></a>進度和完成  
 顯示建立程序的進度。 建立資料庫之後，按一下 [完成]，關閉資料庫精靈並返回 [資料庫] 頁面。 此時會選取新的資料庫，而且您可以檢視並修改它的系統設定。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫組態頁面 &#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [設定 Master Data Services 資料庫和網站](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [資料庫需求 &#40;Master Data Services&#41;](install-windows/database-requirements-master-data-services.md)  
  
  
