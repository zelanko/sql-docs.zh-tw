---
title: "sp_set_database_firewall_rule (Azure SQL Database) |Microsoft 文件"
ms.custom: 
ms.date: 08/04/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_set_database_firewall_rule
- sp_set_database_firewall_rule_TSQL
- sys.sp_set_database_firewall_rule
- sys.sp_set_database_firewall_rule_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_set_database_firewall_rule
- firewall_rules, setting database rules
ms.assetid: 8f0506b6-a4ac-4e4d-91db-8077c40cb17a
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c83057218c015eb9d3488ea730e507ab795ddade
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spsetdatabasefirewallrule-azure-sql-database"></a>sp_set_database_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  建立或更新的資料庫層級防火牆規則您[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 資料庫防火牆規則可以針對設定**主要**資料庫，以及使用者資料庫上[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。 使用自主資料庫使用者時，資料庫防火牆規則會特別有用。 如需詳細資訊，請參閱 [自主的資料庫使用者 - 使資料庫可攜](../../relational-databases/security/contained-database-users-making-your-database-portable.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 **[@name**  =] [N]'*名稱*'  
 用來描述和區分資料庫層級防火牆設定的名稱。 *名稱*是**nvarchar （128)** ，沒有預設值。 Unicode 識別碼`N`是選擇性的[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。 
  
 **[@start_ip_address**  =] '*start_ip_address*'  
 資料庫層級防火牆設定範圍中最低的 IP 位址。 等於或大於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 執行個體。 可能的最低 IP 位址為 `0.0.0.0`。 *start_ip_address*是**varchar （50)** ，沒有預設值。  
  
 [ **@end_ip_address**  =] '*end_ip_address*'  
 資料庫層級防火牆設定範圍中最高的 IP 位址。 等於或小於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 執行個體。 可能的最高 IP 位址為 `255.255.255.255`。 *end_ip_address*是**varchar （50)** ，沒有預設值。  
  
 下表說明支援的引數和選項中[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
> [!NOTE]  
>  Azure 的連線嘗試時，便允許這個欄位和*start_ip_address*欄位等於`0.0.0.0`。  
  
## <a name="remarks"></a>備註  
 資料庫的資料庫層級防火牆設定的名稱必須是唯一的。 如果為預存程序提供的資料庫層級防火牆設定名稱已存在資料庫層級防火牆設定資料表中，則會更新開始和結束 IP 位址。 否則，將會建立新的資料庫層級防火牆設定。  
  
 當您新增的資料庫層級防火牆設定中的開始和結束 IP 位址等於`0.0.0.0`，您可存取您的資料庫中[!INCLUDE[ssSDS](../../includes/sssds-md.md)]從任何 Azure 資源的伺服器。 提供一個值，*名稱*參數，可協助您記住防火牆設定的目的。  
  
## <a name="permissions"></a>Permissions  
 需要**控制項**資料庫的權限。  
  
## <a name="examples"></a>範例  
 下列程式碼會建立資料庫層級防火牆設定稱為`Allow Azure`，可以存取您的資料庫從 Azure。  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 以下程式碼只會針對 IP 位址 `Example DB Setting 1` 建立名為 `0.0.0.4` 的資料庫層級防火牆設定。 然後，`sp_set_database firewall_rule`預存程序呼叫一次，以更新的結束 IP 位址`0.0.0.6`，依此防火牆設定。 這會建立允許 IP 位址的範圍`0.0.0.4`， `0.0.0.5`，和`0.0.0.6`來存取資料庫。
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>請參閱＜  
 [Azure SQL Database 防火牆](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [如何： 設定防火牆設定 (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL Database &#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Azure SQL Database &#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules &#40;Azure SQL Database &#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
