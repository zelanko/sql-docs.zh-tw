---
title: sp_delete_database_firewall_rule （Azure SQL Database） |Microsoft Docs
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
ms.openlocfilehash: 660405e7e7592557422e43655c35ec27c194aad3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68130677"
---
# <a name="sp_delete_database_firewall_rule-azure-sql-database"></a>sp_delete_database_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  從中移除資料庫層級防火牆設定[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 您可以針對 master 資料庫和上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]的使用者資料庫，設定及刪除資料庫防火牆規則。   
  
 
## <a name="syntax"></a>語法  
  
```    
sp_delete_database_firewall_rule [@name =] [N]'name'
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 `[@name =] [N]'name'`  
 要移除的資料庫層級防火牆設定的名稱。 *名稱*為**Nvarchar （128）** ，沒有預設值。 Unicode 識別碼`N`對[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]而言是選擇性的。 
  
## <a name="permissions"></a>權限  
 只有由布建程式所建立的伺服器層級主體登入或指派為系統管理員的 Azure Active Directory 主體，才可以刪除資料庫層級防火牆規則。  
  
## <a name="example"></a>範例  
 下列範例會移除名為`Example DB Setting 1`的資料庫層級防火牆設定。
  
```  
-- Remove database-level firewall setting  
EXECUTE sp_delete_database_firewall_rule N'Example DB Setting 1';  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Azure SQL Database 防火牆](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [如何：設定防火牆設定（Azure SQL Database）](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_set_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)   
 [database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  


