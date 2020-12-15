---
description: sp_set_database_firewall_rule (Azure SQL Database)
title: sp_set_database_firewall_rule
titleSuffix: Azure SQL Database
ms.date: 08/04/2017
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_database_firewall_rule
- sp_set_database_firewall_rule_TSQL
- sys.sp_set_database_firewall_rule
- sys.sp_set_database_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_database_firewall_rule
- firewall_rules, setting database rules
ms.assetid: 8f0506b6-a4ac-4e4d-91db-8077c40cb17a
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current
ms.custom: seo-dt-2019
ms.openlocfilehash: edbe51dc6694a94fcf68b012153e065906ce2208
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472639"
---
# <a name="sp_set_database_firewall_rule-azure-sql-database"></a>sp_set_database_firewall_rule (Azure SQL Database)
[!INCLUDE[Azure SQL Database](../../includes/applies-to-version/asdb.md)]

  建立或更新您的資料庫層級防火牆規則 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。 您可以針對 **master** 資料庫和使用者資料庫，設定資料庫防火牆規則 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。 使用自主資料庫使用者時，資料庫防火牆規則特別有用。 如需詳細資訊，請參閱 [自主資料庫使用者 - 使資料庫可攜](../../relational-databases/security/contained-database-users-making-your-database-portable.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
`[ @name = ] [N]'name'` 用來描述和區分資料庫層級防火牆設定的名稱。 *名稱* 是 **Nvarchar (128)** 沒有預設值。 的 Unicode 識別碼 `N` 是選擇性的 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 。 
  
`[ @start_ip_address = ] 'start_ip_address'` 資料庫層級防火牆設定範圍中最低的 IP 位址。 等於或大於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 執行個體。 可能的最低 IP 位址為 `0.0.0.0`。 *start_ip_address* 是 **Varchar (50)** 沒有預設值。  
  
`[ @end_ip_address = ] 'end_ip_address'` 資料庫層級防火牆設定範圍中最高的 IP 位址。 等於或小於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 執行個體。 可能的最高 IP 位址為 `255.255.255.255`。 *end_ip_address* 是 **Varchar (50)** 沒有預設值。  
  
 下表示范中支援的引數和選項 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。  
  
> [!NOTE]  
>  當這個欄位和 [ *start_ip_address* ] 欄位等於時，便允許 Azure 連接嘗試 `0.0.0.0` 。  
  
## <a name="remarks"></a>備註  
 資料庫的資料庫層級防火牆設定的名稱必須是唯一的。 如果為預存程序提供的資料庫層級防火牆設定名稱已存在資料庫層級防火牆設定資料表中，則會更新開始和結束 IP 位址。 否則，將會建立新的資料庫層級防火牆設定。  
  
 當您加入的資料庫層級防火牆設定中的開始和結束 IP 位址等於時 `0.0.0.0` ，您就可以 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 從任何 Azure 資源存取伺服器中的資料庫。 提供值給 *名稱* 參數，協助您記住防火牆設定的用途。  
  
## <a name="permissions"></a>權限  
 需要資料庫上的 **CONTROL** 權限。  
  
## <a name="examples"></a>範例  
 下列程式碼會建立名為 `Allow Azure` 的資料庫層級防火牆設定，該設定可讓您從 Azure 存取您的資料庫。  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 以下程式碼只會針對 IP 位址 `Example DB Setting 1` 建立名為 `0.0.0.4` 的資料庫層級防火牆設定。 然後， `sp_set_database firewall_rule` 再次呼叫預存 `0.0.0.6` 程式，在該防火牆設定中將結束 IP 位址更新為。 這會建立一個範圍，允許 IP 位址 `0.0.0.4` 、 `0.0.0.5` 和 `0.0.0.6` 存取資料庫。
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Azure SQL Database 防火牆](/azure/azure-sql/database/firewall-configure)   
 [如何： (Azure SQL Database) 設定防火牆設定 ](/azure/azure-sql/database/firewall-configure)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [sys.database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
