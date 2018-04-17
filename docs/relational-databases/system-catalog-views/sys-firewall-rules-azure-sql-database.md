---
title: sys.firewall_rules （SQL Azure 資料庫） |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.firewall_rules
- firewall_rules
- sys.firewall_rules_TSQL
- firewall_rules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- firewall_rules
- sys.firewall_rules
ms.assetid: 140d2cd8-9aa1-4cc5-870d-e1dbc873b3fe
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 3f3f25541c1c60e4a9dad3dcfdaff037c7a7bcde
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysfirewallrules-azure-sql-database"></a>sys.firewall_rules (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回與相關聯的伺服器層級防火牆設定的相關資訊您[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 `sys.firewall_rules` 檢視表包含下列資料行：  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|id|**INT**|伺服器層級防火牆設定的識別碼。|  
|name|**NVARCHAR （128)**|您選擇用來描述和區分伺服器層級防火牆設定的名稱。|  
|start_ip_address|**VARCHAR （50)**|伺服器層級防火牆設定範圍中最低的 IP 位址。 等於或大於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器。 可能的最低 IP 位址為 `0.0.0.0`。|  
|end_ip_address|**VARCHAR （50)**|伺服器層級防火牆設定範圍中最高的 IP 位址。 等於或小於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器。 可能的最高 IP 位址為 `255.255.255.255`。<br /><br /> 注意： Windows Azure 連接嘗試時，便允許這個欄位和**start_ip_address**欄位等於`0.0.0.0`。|  
|create_date|**日期時間**|建立伺服器層級防火牆設定時的 UTC 日期和時間。<br /><br /> 注意： UTC 是國際標準時間的縮略字。|  
|modify_date|**日期時間**|上次修改伺服器層級防火牆設定時的 UTC 日期和時間。|  
  
## <a name="remarks"></a>備註  
 若要移除資料庫防火牆規則，請使用[sp_delete_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)。 若要設定單一資料庫的防火牆規則，請參閱[sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)。 若要傳回現有防火牆規則的相關資訊，請查詢 sys.firewall_rules （SQL Azure 資料庫）。  
  
## <a name="permissions"></a>Permissions  
 此檢視的唯讀存取可供所有使用者只要具有權限連接到**主要**資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [設定用於 Database Engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configure a Firewall for FILESTREAM 存取](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)   
 [設定供報表伺服器存取的防火牆](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)   
 [如何：設定防火牆設定 (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)  
  
  
