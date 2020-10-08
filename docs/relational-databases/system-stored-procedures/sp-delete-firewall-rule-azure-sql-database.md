---
description: sp_delete_firewall_rule (Azure SQL Database)
title: sp_delete_firewall_rule
titleSuffix: Azure SQL Database
ms.date: 07/27/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_firewall_rule_TSQL
- sp_delete_firewall_rule
- sys.sp_delete_firewall_rule
- sys.sp_delete_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_firewall_rule procedure
ms.assetid: cf93eed1-ba97-4850-9fcc-b9c5a9317908
author: VanMSFT
ms.author: vanto
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 3b88db4894b7d24599ccade131fdf2de7fd82d9b
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810305"
---
# <a name="sp_delete_firewall_rule-azure-sql-database"></a>sp_delete_firewall_rule (Azure SQL Database)
[!INCLUDE [asdb-asa](../../includes/applies-to-version/asdb-asa.md)]

  從您的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器移除伺服器層級防火牆設定。 這個預存程序只可在 master 資料庫中對伺服器層級主體登入提供。  

  
## <a name="syntax"></a>語法  
  
```  
sp_delete_firewall_rule [@name =] 'name' 
[ ; ] 
```  
  
## <a name="arguments"></a>引數  
 此預存程序的引數為：  
  
 [ @name =] '*name*'  
 要移除的伺服器層級防火牆設定的名稱。 *名稱* 是 **Nvarchar (128) ** ，沒有預設值。  
  
## <a name="remarks"></a>備註  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，驗證連線需要登入資料，且伺服器層級防火牆規則會暫時快取在每個資料庫中。 此快取會定期重新整理。 若要重新整理驗證快取，並確定資料庫擁有登入資料表的最新版本，請執行 [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 只有由佈建程序所建立的伺服器層級主體登入才可以刪除伺服器層級防火牆規則。 使用者必須連接至 master 資料庫，才能執行 sp_delete_firewall_rule。  
  
## <a name="example"></a>範例  
 以下範例會移除名為 'Example setting 1' 的伺服器層級防火牆設定。 在虛擬 master 資料庫中執行語句。  
  
```   
EXEC sp_delete_firewall_rule N'Example setting 1';   
```  
  
## <a name="see-also"></a>另請參閱  
 [Azure SQL Database 防火牆](/azure/azure-sql/database/firewall-configure)   
 [如何： (Azure SQL Database) 設定防火牆設定 ](/azure/azure-sql/database/firewall-configure)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sys.firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
  
