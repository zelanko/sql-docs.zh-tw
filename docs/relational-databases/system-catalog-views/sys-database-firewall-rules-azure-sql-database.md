---
title: "sys.database_firewall_rules (Azure SQL Database) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.database_firewall_rules_TSQL
- database_firewall_rules_TSQL
- sys.database_firewall_rules
- database_firewall_rules
dev_langs:
- TSQL
helpviewer_keywords:
- database_firewall_rules
- sys.database_firewall_rules
ms.assetid: 2e821593-3b9f-43d6-a99b-1ceffe177faf
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c598371c8df7a92622ec43700fc504b082640e1f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatabasefirewallrules-azure-sql-database"></a>sys.database_firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回與相關聯的資料庫層級防火牆設定的相關資訊您[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 使用自主的資料庫使用者時，資料庫層級防火牆設定特別有用。 如需詳細資訊，請參閱 [自主的資料庫使用者 - 使資料庫可攜](../../relational-databases/security/contained-database-users-making-your-database-portable.md)。  
  
 `sys.database_firewall_rules` 檢視表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|id|**整數**|資料庫層級防火牆設定的識別碼。|  
|name|**NVARCHAR （128)**|您選擇用來描述和區分資料庫層級防火牆設定的名稱。|  
|start_ip_address|**VARCHAR （50)**|資料庫層級防火牆設定範圍中最低的 IP 位址。 等於或大於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 執行個體。 可能的最低 IP 位址為 `0.0.0.0`。|  
|end_ip_address|**VARCHAR （50)**|防火牆設定範圍中最高的 IP 位址。 等於或小於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 執行個體。 可能的最高 IP 位址為 `255.255.255.255`。<br /><br /> 注意： Windows Azure 連接嘗試時，便允許這個欄位和**start_ip_address**欄位等於`0.0.0.0`。|  
|create_date|**日期時間**|建立資料庫層級防火牆設定時的 UTC 日期和時間。|  
|modify_date|**日期時間**|上次修改資料庫層級防火牆設定時的 UTC 日期和時間。|  
  
## <a name="remarks"></a>備註  
 若要移除資料庫防火牆規則，請使用[sp_delete_database_firewall_rule &#40;Azure SQL Database &#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md). 若要設定防火牆規則的所有[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，請參閱[sp_set_firewall_rule &#40;Azure SQL Database &#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md). 若要傳回的防火牆規則的現有資料庫的相關資訊，請查詢[sys.database_firewall_rules (Azure SQL Database)](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)。  
  
## <a name="permissions"></a>Permissions  
 此檢視位於**主要**資料庫及每個使用者資料庫。 這個檢視表的唯讀存取權可提供給有權連接至資料庫的所有使用者。  
  
## <a name="see-also"></a>請參閱＜  
 [sp_set_firewall_rule &#40;Azure SQL Database &#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules (Azure SQL Database)](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Azure SQL Database &#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [設定用於 Database Engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configure a Firewall for FILESTREAM 存取](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)   
 [設定供報表伺服器存取的防火牆](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
  
