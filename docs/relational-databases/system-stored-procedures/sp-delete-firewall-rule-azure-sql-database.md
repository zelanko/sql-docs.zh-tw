---
title: "sp_delete_firewall_rule （SQL Azure 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 07/27/2016
ms.prod: 
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: 
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_delete_firewall_rule_TSQL
- sp_delete_firewall_rule
- sys.sp_delete_firewall_rule
- sys.sp_delete_firewall_rule_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_delete_firewall_rule procedure
ms.assetid: cf93eed1-ba97-4850-9fcc-b9c5a9317908
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa2815c27668bc680ce5da72b6713e29b517f43b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spdeletefirewallrule-azure-sql-database"></a>sp_delete_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  從您的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器移除伺服器層級防火牆設定。 這個預存程序只可在 master 資料庫中對伺服器層級主體登入提供。  

  
## <a name="syntax"></a>語法  
  
```  
sp_delete_firewall_rule [@name =] 'name' 
[ ; ] 
```  
  
## <a name="arguments"></a>引數  
 此預存程序的引數為：  
  
 [@name =] '*名稱*'  
 要移除的伺服器層級防火牆設定的名稱。 *名稱*是**nvarchar (128)**沒有預設值。  
  
## <a name="remarks"></a>備註  
 在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]、 驗證連線所需的登入資料和伺服器層級防火牆規則中每個資料庫會暫時快取。 此快取會定期重新整理。 若要強制驗證快取重新整理，並請確定資料庫有登入資料表的最新版本，執行[DBCC FLUSHAUTHCACHE &#40;TRANSACT-SQL &#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 只有由佈建程序所建立的伺服器層級主體登入才可以刪除伺服器層級防火牆規則。 使用者必須連接到 master 資料庫來執行 sp_delete_firewall_rule。  
  
## <a name="example"></a>範例  
 以下範例會移除名為 'Example setting 1' 的伺服器層級防火牆設定。 虛擬 master 資料庫中執行陳述式。  
  
```   
EXEC sp_delete_firewall_rule N'Example setting 1';   
```  
  
## <a name="see-also"></a>請參閱＜  
 [Azure SQL Database 防火牆](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [如何： 設定防火牆設定 (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL Database &#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sys.firewall_rules &#40;Azure SQL Database &#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
  
  


