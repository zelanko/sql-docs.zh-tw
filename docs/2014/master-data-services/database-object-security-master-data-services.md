---
title: 資料庫物件安全性 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- database [Master Data Services], object security
- security [Master Data Services], database objects
ms.assetid: dd5ba503-7607-45d9-ad0d-909faaade179
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3eafc9720197ffc32cdca2ef58f91725befaaec1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483156"
---
# <a name="database-object-security-master-data-services"></a>資料庫物件安全性 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中，資料儲存在多個資料庫資料表並且顯示在檢視表中。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式中受到保護的資訊，對具有 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫存取權的使用者是可見的。  
  
 具體來說，員工薪資資訊可能包含在 Employee 模型中，公司財務資訊可能包含在 Account 模型中。 您可以在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 使用者介面中拒絕使用者存取這些模型，但具有資料庫存取權的使用者可以檢視此資料。  
  
 您可以授與資料庫物件權限，讓特定資料供使用者使用。 如需授與權限的詳細資訊，請參閱 [GRANT 物件權限 &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql)。 如需保護 SQL Server 安全的詳細資訊，請參閱 [保護 SQL Server 的安全](../relational-databases/security/securing-sql-server.md)。  
  
 下列工作需要存取 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫：  
  
-   [暫存資料](#Staging)  
  
-   [依商務規則驗證資料](#rules)  
  
-   [刪除版本](#Versions)  
  
-   [立即套用階層成員權限](#Hierarchy)  
  
-   [變更系統管理員帳戶](#SysAdmin)  
  
-   [設定系統設定](#SysSettings)  
  
##  <a name="staging-data"></a><a name="Staging"></a> 暫存資料  
 在下表中，每個安全物件都會有 "name" 作為名稱的一部分。 這表示建立實體時所指定的暫存資料表名稱。 如需詳細資訊，請參閱[資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)  
  
|動作|安全性實體|權限|  
|------------|----------------|-----------------|  
|將分葉成員及其屬性載入至暫存資料表。|stg.name_Leaf|必要：INSERT<br /><br /> 選擇性：SELECT 和 UPDATE|  
|將資料從 [分葉] 暫存資料表載入至適當的 MDS 資料庫資料表。|stg.udp_name_Leaf|執行 CREATE 陳述式之前，請先執行|  
|將合併成員及其屬性載入至暫存資料表。|stg.name_Consolidated|必要：INSERT<br /><br /> 選擇性：SELECT 和 UPDATE|  
|將資料從 [合併] 暫存資料表載入至適當的 MDS 資料庫資料表。|stg.udp_name_Consolidated|執行 CREATE 陳述式之前，請先執行|  
|在明確階層中，將分葉和合併成員的關聯性載入至臨時表。|stg.name_Relationship|必要：INSERT<br /><br /> 選擇性：SELECT 和 UPDATE|  
|將資料從 [關聯性] 暫存資料表載入至適當的 MDS 資料表。|stg.udp_name_Relationship|執行 CREATE 陳述式之前，請先執行|  
|檢視將資料從暫存資料表插入至 MDS 資料庫資料表時發生的錯誤。|stg.udp_name_Relationship|SELECT|  
  
 如需詳細資訊，請參閱[資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)。  
  
##  <a name="validating-data-against-business-rules"></a><a name="rules"></a>根據商務規則驗證資料  
  
|動作|安全性實體|權限|  
|------------|---------------|-----------------|  
|依商務規則驗證資料版本|mdm.udpValidateModel|執行 CREATE 陳述式之前，請先執行|  
  
 如需詳細資訊，請參閱 [驗證預存程序 &#40;Master Data Services&#41;](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)。  
  
##  <a name="deleting-versions"></a><a name="Versions"></a>刪除版本  
  
|動作|安全性實體|權限|  
|------------|----------------|-----------------|  
|決定要刪除之版本的識別碼|mdm.viw_SYSTEM_SCHEMA_VERSION|SELECT|  
|刪除模型的版本|mdm.udpVersionDelete|執行 CREATE 陳述式之前，請先執行|  
  
 如需詳細資訊，請參閱[刪除版本 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-version-master-data-services.md)。  
  
##  <a name="immediately-applying-hierarchy-member-permissions"></a><a name="Hierarchy"></a>立即套用階層成員許可權  
  
|動作|安全性實體|權限|  
|------------|----------------|-----------------|  
|立即套用成員權限|mdm.udpSecurityMemberProcessRebuildModel|執行 CREATE 陳述式之前，請先執行|  
  
 如需詳細資訊，請參閱[立即套用成員權限 &#40;Master Data Services&#41;](../../2014/master-data-services/immediately-apply-member-permissions-master-data-services.md)。  
  
##  <a name="changing-the-system-administrator-account"></a><a name="SysAdmin"></a>變更系統管理員帳戶  
  
|動作|安全性實體|權限|  
|------------|----------------|-----------------|  
|決定新管理員的 SID|mdm.tblUser|SELECT|  
|變更系統管理員帳戶|mdm.udpSecuritySetAdministrator|執行 CREATE 陳述式之前，請先執行|  
  
 如需詳細資訊，請參閱[將系統管理員帳戶變更 &#40;Master Data Services&#41;](../../2014/master-data-services/change-the-system-administrator-account-master-data-services.md)。  
  
##  <a name="configuring-system-settings"></a><a name="SysSettings"></a>正在進行系統設定  
 有些系統設定可設定控制 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]的行為。 您可以在 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 中調整這些設定；如果您有 UPDATE 存取權，也可以直接在 mdm.tblSystemSetting 資料庫資料表中調整這些設定。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [安全性 &#40;Master Data Services&#41;](../../2014/master-data-services/security-master-data-services.md)  
  
  
