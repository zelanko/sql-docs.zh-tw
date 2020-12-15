---
description: sp_set_firewall_rule (Azure SQL Database)
title: sp_set_firewall_rule (Azure SQL Database) Microsoft Docs
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
monikerRange: = azuresqldb-current || = azure-sqldw-latest
ms.openlocfilehash: 795aeb9a03f839cae400e92060ac21056f314d2f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468279"
---
# <a name="sp_set_firewall_rule-azure-sql-database"></a>sp_set_firewall_rule (Azure SQL Database)
[!INCLUDE [asdb-asa](../../includes/applies-to-version/asdb-asa.md)]

  建立或更新 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器的伺服器層級防火牆設定。 這個預存程式只能在 master 資料庫中提供給伺服器層級主體登入或指派 Azure Active Directory 主體。  
  
  
## <a name="syntax"></a>語法  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 下表示范中支援的引數和選項 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。  
  
|名稱|Datatype|描述|  
|----------|--------------|-----------------|  
|[ @name =] ' name '|**NVARCHAR (128)**|用來描述和區分伺服器層級防火牆設定的名稱。|  
|[ @start_ip_address =] ' start_ip_address '|**VARCHAR (50)**|伺服器層級防火牆設定範圍中最低的 IP 位址。 等於或大於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器。 可能的最低 IP 位址為 `0.0.0.0`。|  
|[ @end_ip_address =] ' end_ip_address '|**VARCHAR (50)**|伺服器層級防火牆設定範圍中最高的 IP 位址。 等於或小於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器。 可能的最高 IP 位址為 `255.255.255.255`。<br /><br /> 注意：當這個欄位和 [ *start_ip_address* ] 欄位等於時，便允許 Azure 連接嘗試 `0.0.0.0` 。|  
  
## <a name="remarks"></a>備註  
 伺服器層級防火牆設定的名稱必須是唯一的。 如果為預存程序提供的設定名稱已存在防火牆設定資料表中，則會更新開始和結束 IP 位址。 否則，將會建立新的伺服器層級防火牆設定。  
  
 如果您加入的伺服器層級防火牆設定中的開始和結束 IP 位址等於 `0.0.0.0`，表示可從 Azure 存取您的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器。 提供值給 *名稱* 參數，協助您記住伺服器層級防火牆設定的用途。  
  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，驗證連線需要登入資料，且伺服器層級防火牆規則會暫時快取在每個資料庫中。 此快取會定期重新整理。 若要重新整理驗證快取，並確定資料庫擁有登入資料表的最新版本，請執行 [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 只有布建程式所建立的伺服器層級主體登入或指派為系統管理員 Azure Active Directory 主體，才能建立或修改伺服器層級防火牆規則。 使用者必須連接至 master 資料庫，才能執行 sp_set_firewall_rule。  
  
## <a name="examples"></a>範例  
 下列程式碼會建立名為 `Allow Azure` 的伺服器層級防火牆設定，該設定可讓您從 Azure 進行存取。 在虛擬 master 資料庫中執行下列動作。  
  
```  
-- Enable Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 以下程式碼只會針對 IP 位址 `Example setting 1` 建立名為 `0.0.0.2` 的伺服器層級防火牆設定。 然後， `sp_set_firewall_rule` 再次呼叫預存 `0.0.0.4` 程式，在該防火牆設定中將結束 IP 位址更新為。 這會建立一個範圍，允許 IP 位址 `0.0.0.2` 、 `0.0.0.3` 和 `0.0.0.4` 存取伺服器。  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Azure SQL Database 防火牆](/azure/azure-sql/database/firewall-configure)   
 [如何： (Azure SQL Database) 設定防火牆設定 ](/azure/azure-sql/database/firewall-configure)   
 [sys.firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)