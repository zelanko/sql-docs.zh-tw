---
title: sp_delete_database_firewall_rule (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 08/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_database_firewall_rule
- sp_delete_database_firewall_rule_TSQL
- sys.sp_delete_database_firewall_rule
- sys.sp_delete_database_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_database_firewall_rule procedure
ms.assetid: ed295312-e586-4fc2-9e80-806b490ee7bd
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 225d5d7571e213308de337240ec8a0897f074a6a
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43037482"
---
# <a name="spdeletedatabasefirewallrule-azure-sql-database"></a>sp_delete_database_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  移除資料庫層級防火牆設定，從您[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 資料庫防火牆規則可以設定和刪除 master 資料庫，以及使用者資料庫上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。   
  
 
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_database_firewall_rule [@name =] [N]'name'
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@name =**] **'***名稱***'**  
 要移除的資料庫層級防火牆設定的名稱。 *名稱*已 **& lt;languagekeyword>nvarchar(128)</languagekeyword>** ，沒有預設值。 Unicode 識別碼`N`都是選擇性的[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。 
  
## <a name="permissions"></a>Permissions  
 只有伺服器層級主體登入建立的佈建程序或 Azure Active Directory 主體指派為系統管理員可以刪除資料庫層級防火牆規則。  
  
## <a name="example"></a>範例  
 下列範例會移除資料庫層級防火牆設定，稱為`Example DB Setting 1`。
  
```  
-- Remove database-level firewall setting  
EXECUTE sp_delete_database_firewall_rule N'Example DB Setting 1';  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Azure SQL Database 防火牆](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [如何： 設定防火牆設定 (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_set_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  


