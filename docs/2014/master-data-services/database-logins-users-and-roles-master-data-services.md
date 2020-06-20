---
title: 資料庫登入、使用者和角色 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- security [Master Data Services], database roles
- database [Master Data Services], users
- security [Master Data Services], database users
- database [Master Data Services], roles
- database [Master Data Services], logins
- security [Master Data Services], database logins
ms.assetid: 72ee383e-a619-461b-9f9d-1cac162ab0c5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 416ae500d940eb31eee3294edd07c289b124b6c4
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971648"
---
# <a name="database-logins-users-and-roles-master-data-services"></a>資料庫登入、使用者和角色 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 包含的登入、使用者和角色會自動安裝在主控 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 資料庫的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 執行個體上。 不應對這些登入、使用者和角色進行修改。  
  
## <a name="logins"></a>登入  
  
|登入|描述|  
|-----------|-----------------|  
|`mds_dlp_login`|允許建立 UNSAFE 組件。<br /><br /> -具有隨機產生之密碼的已停用登入。<br /><br /> -對應至 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的 dbo。<br /><br /> -若是 msdb，mds_clr_user 會對應至此登入。<br /><br /> <br /><br /> 如需詳細資訊，請參閱 [建立組件](../relational-databases/clr-integration/assemblies/creating-an-assembly.md)。|  
|`mds_email_login`|用於通知的已啟用登入。<br /><br /> 若是 msdb 和 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫，mds_email_user 會對應至此登入。|  
  
## <a name="msdb-users"></a>msdb 使用者  
  
|User|描述|  
|----------|-----------------|  
|`mds_clr_user`|未使用。<br /><br /> 對應至 mds_dlp_login。|  
|`mds_email_user`|用於通知。<br /><br /> 對應至 mds_email_login。<br /><br /> 為 DatabaseMailUserRole 角色的成員。|  
  
## <a name="master-data-services-database-users"></a>Master Data Services 資料庫使用者  
  
|User|描述|  
|----------|-----------------|  
|`mds_email_user`|用於通知。<br /><br /> 具有 mdm 結構描述的 SELECT 權限。<br /><br /> 具有 mdm.MemberGetCriteria 使用者定義資料表類型的 EXECUTE 權限。<br /><br /> 具有 mdm.udpNotificationQueueActivate 預存程序的 EXECUTE 權限。|  
|**mds_schema_user**|擁有 mdm 和 mdq 結構描述。 預設結構描述為 mdm。<br /><br /> 沒有對應的登入。|  
|**mds_ssb_user**|用來執行 Service Broker 工作。<br /><br /> 具有所有結構描述的 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE 權限。<br /><br /> 沒有對應的登入。|  
  
## <a name="master-data-services-database-role"></a>Master Data Services 資料庫角色  
  
|角色|描述|  
|----------|-----------------|  
|`mds_exec`|這個角色包含當您建立 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] Web 應用程式並指定應用程式集區的帳戶時，在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中指定的帳戶。 mds_exec 角色具有：<br /><br /> 所有架構的**EXECUTE**許可權。<br /><br /> 這些資料表的**ALTER**、 **INSERT**和**SELECT**許可權：<br />mdm.tblStgMember<br />mdm.tblStgMemberAttribute<br />mdm.tbleStgRelationship<br /><br /> 這些資料表的**SELECT**許可權：<br />mdm.tblUser<br />mdm.tblUserGroup<br />mdm.tblUserPreference<br /><br /> **選取**這些 views 的許可權：<br />mdm.viw_SYSTEM_SECURITY_NAVIGATION<br />mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL<br />mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL_MEMBER<br />mdm.viw_SYSTEM_SECURITY_USER_MODEL|  
  
## <a name="schemas"></a>結構描述  
  
|角色|描述|  
|----------|-----------------|  
|`mdm`|包含所有 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫與 Service Broker 物件，而非 mdq 結構描述中包含的函數。|  
|`mdq`|包含 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫函數，這些函數與根據規則運算式或相似度篩選成員結果有關，而且可用於格式化通知電子郵件。|  
|**stg**|包含 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫資料表、預存程序以及與暫存處理序有關的檢視表。 請勿刪除這些物件的任何一個。 如需暫存進程的詳細資訊，請參閱[資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [資料庫物件安全性 &#40;Master Data Services&#41;](../../2014/master-data-services/database-object-security-master-data-services.md)  
  
  
