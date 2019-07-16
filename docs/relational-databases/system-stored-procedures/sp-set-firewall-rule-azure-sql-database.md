---
title: sp_set_firewall_rule (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 436396ed0982b12fffd5b894cb4c2a4006484ab0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104419"
---
# <a name="spsetfirewallrule-azure-sql-database"></a>sp_set_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  建立或更新 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器的伺服器層級防火牆設定。 只有伺服器層級主體登入或已指派的 Azure Active Directory 主體的 master 資料庫中使用這個預存程序。  
  
  
## <a name="syntax"></a>語法  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 下表示範支援的引數和選項[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
|名稱|資料類型|描述|  
|----------|--------------|-----------------|  
|[@name =] 'name'|**NVARCHAR(128)**|用來描述和區分伺服器層級防火牆設定的名稱。|  
|[@start_ip_address =] 'start_ip_address'|**VARCHAR(50)**|伺服器層級防火牆設定範圍中最低的 IP 位址。 等於或大於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器。 可能的最低 IP 位址為 `0.0.0.0`。|  
|[@end_ip_address =] 'end_ip_address'|**VARCHAR(50)**|伺服器層級防火牆設定範圍中最高的 IP 位址。 等於或小於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器。 可能的最高 IP 位址為 `255.255.255.255`。<br /><br /> 注意:Azure 的連線嘗試時，便允許這個欄位並*start_ip_address*欄位等於`0.0.0.0`。|  
  
## <a name="remarks"></a>備註  
 伺服器層級防火牆設定的名稱必須是唯一的。 如果為預存程序提供的設定名稱已存在防火牆設定資料表中，則會更新開始和結束 IP 位址。 否則，將會建立新的伺服器層級防火牆設定。  
  
 當您加入伺服器層級防火牆設定中的開始和結束 IP 位址等於`0.0.0.0`，可存取您[!INCLUDE[ssSDS](../../includes/sssds-md.md)]從 Azure 的伺服器。 提供一個值*名稱*參數，將會幫助您記住伺服器層級防火牆設定的目的。  
  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，驗證連線需要登入資料，且伺服器層級防火牆規則會暫時快取在每個資料庫中。 此快取會定期重新整理。 若要重新整理驗證快取，並確定資料庫擁有登入資料表的最新版本，請執行 [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 只有伺服器層級主體登入建立的佈建程序或 Azure Active Directory 主體指派為系統管理員可以建立或修改伺服器層級防火牆規則。 使用者必須連接到 master 資料庫執行 sp_set_firewall_rule。  
  
## <a name="examples"></a>範例  
 下列程式碼會建立伺服器層級防火牆設定稱為`Allow Azure`，可讓您從 Azure 的存取。 執行下列命令在虛擬 master 資料庫中。  
  
```  
-- Enable Windows Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 以下程式碼只會針對 IP 位址 `Example setting 1` 建立名為 `0.0.0.2` 的伺服器層級防火牆設定。 然後，`sp_set_firewall_rule`預存程序來更新 結束 IP 位址會再次呼叫`0.0.0.4`，依此防火牆設定。 這會建立可讓 IP 位址範圍`0.0.0.2`， `0.0.0.3`，和`0.0.0.4`來存取伺服器。  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Azure SQL Database 防火牆](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [如何：設定防火牆設定 (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sys.firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
