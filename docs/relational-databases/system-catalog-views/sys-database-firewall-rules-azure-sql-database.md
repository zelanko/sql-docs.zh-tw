---
title: database_firewall_rules (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-database
ms.reviewer: ''
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
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 61402b762b7a6b4d944214d59e187e1457e93f93
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155773"
---
# <a name="sysdatabase_firewall_rules-azure-sql-database"></a>sys.database_firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回與您[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]的相關聯的資料庫層級防火牆設定資訊。 使用自主的資料庫使用者時，資料庫層級防火牆設定特別有用。 如需詳細資訊，請參閱 [自主的資料庫使用者 - 使資料庫可攜](../../relational-databases/security/contained-database-users-making-your-database-portable.md)。  
  
 `sys.database_firewall_rules` 檢視表包含下列資料行：  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|id|**INTEGER**|資料庫層級防火牆設定的識別碼。|  
|name|**NVARCHAR(128)**|您選擇用來描述和區分資料庫層級防火牆設定的名稱。|  
|start_ip_address|**VARCHAR(45)**|資料庫層級防火牆設定範圍中最低的 IP 位址。 等於或大於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 執行個體。 可能的最低 IP 位址為 `0.0.0.0`。|  
|end_ip_address|**VARCHAR(45)**|防火牆設定範圍中最高的 IP 位址。 等於或小於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 執行個體。 可能的最高 IP 位址為 `255.255.255.255`。<br /><br /> 注意：當此欄位和**start_ip_address**欄位等於`0.0.0.0`時, 允許 Azure 連接嘗試。|  
|create_date|**從中**|建立資料庫層級防火牆設定時的 UTC 日期和時間。|  
|modify_date|**從中**|上次修改資料庫層級防火牆設定時的 UTC 日期和時間。|  
  
## <a name="remarks"></a>備註  
 若要傳回與您的 Microsoft Azure SQL Database 相關聯之伺服器層級防火牆設定的資訊, 請使用[firewall_rules (Azure SQL Database)](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)。  
  
## <a name="permissions"></a>Permissions  
 這個視圖會在**master**資料庫和每個使用者資料庫中提供。 這個檢視表的唯讀存取權可提供給有權連接至資料庫的所有使用者。  
  
## <a name="see-also"></a>另請參閱
[sp_set_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
[設定資料庫引擎存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[為 FILESTREAM 存取設定防火牆](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[設定供報表伺服器存取的防火牆](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
