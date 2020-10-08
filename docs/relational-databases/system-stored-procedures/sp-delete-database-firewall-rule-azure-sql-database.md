---
description: sp_delete_database_firewall_rule (Azure SQL Database)
title: sp_delete_database_firewall_rule (Azure SQL Database) Microsoft Docs
ms.custom: ''
ms.date: 08/04/2017
ms.service: sql-database
ms.reviewer: ''
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: f4a3a7a16ed2f222a7d179cbae17b6bdfb2982f5
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810322"
---
# <a name="sp_delete_database_firewall_rule-azure-sql-database"></a>sp_delete_database_firewall_rule (Azure SQL Database)
[!INCLUDE[Azure SQL Database](../../includes/applies-to-version/asdb.md)]

  從移除資料庫層級防火牆設定 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。 您可以針對 master 資料庫以及的使用者資料庫，設定和刪除資料庫防火牆規則 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 。   
  
 
## <a name="syntax"></a>語法  
  
```    
sp_delete_database_firewall_rule [@name =] [N]'name'
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 `[@name =] [N]'name'`  
 要移除的資料庫層級防火牆設定的名稱。 *名稱* 是 **Nvarchar (128) ** 沒有預設值。 的 Unicode 識別碼 `N` 是選擇性的 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 。 
  
## <a name="permissions"></a>權限  
 只有布建程式所建立的伺服器層級主體登入或指派為系統管理員 Azure Active Directory 主體，才能刪除資料庫層級的防火牆規則。  
  
## <a name="example"></a>範例  
 下列範例會移除名為的資料庫層級防火牆設定 `Example DB Setting 1` 。
  
```  
-- Remove database-level firewall setting  
EXECUTE sp_delete_database_firewall_rule N'Example DB Setting 1';  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Azure SQL Database 防火牆](/azure/azure-sql/database/firewall-configure)   
 [如何： (Azure SQL Database) 設定防火牆設定 ](/azure/azure-sql/database/firewall-configure)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_set_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
