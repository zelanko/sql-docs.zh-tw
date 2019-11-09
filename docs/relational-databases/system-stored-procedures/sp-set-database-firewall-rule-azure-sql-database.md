---
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 2a465e03c3b77b8d05437fa0cfaf3354434ce973
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843847"
---
# <a name="sp_set_database_firewall_rule-azure-sql-database"></a>sp_set_database_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  建立或更新 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]的資料庫層級防火牆規則。 您可以針對**master**資料庫和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]上的使用者資料庫設定資料庫防火牆規則。 使用自主資料庫使用者時，資料庫防火牆規則特別有用。 如需詳細資訊，請參閱 [自主資料庫使用者 - 使資料庫可攜](../../relational-databases/security/contained-database-users-making-your-database-portable.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 **[@name** =] [N] '*name*'  
 用來描述和區分資料庫層級防火牆設定的名稱。 *名稱*為**Nvarchar （128）** ，沒有預設值。 Unicode 識別碼 `N` 對於 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]而言是選擇性的。 
  
 **[@start_ip_address** =]'*start_ip_address*'  
 資料庫層級防火牆設定範圍中最低的 IP 位址。 等於或大於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 執行個體。 可能的最低 IP 位址為 `0.0.0.0`。 *start_ip_address*為**Varchar （50）** ，沒有預設值。  
  
 [ **@end_ip_address** =]'*end_ip_address*'  
 資料庫層級防火牆設定範圍中最高的 IP 位址。 等於或小於這個位址的 IP 位址可以嘗試連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 執行個體。 可能的最高 IP 位址為 `255.255.255.255`。 *end_ip_address*為**Varchar （50）** ，沒有預設值。  
  
 下表示范 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中支援的引數和選項。  
  
> [!NOTE]  
>  當此欄位和*start_ip_address*欄位等於 `0.0.0.0`時，允許 Azure 連線嘗試。  
  
## <a name="remarks"></a>備註  
 資料庫的資料庫層級防火牆設定的名稱必須是唯一的。 如果為預存程序提供的資料庫層級防火牆設定名稱已存在資料庫層級防火牆設定資料表中，則會更新開始和結束 IP 位址。 否則，將會建立新的資料庫層級防火牆設定。  
  
 當您新增資料庫層級防火牆設定，其中的開始和結束 IP 位址等於 `0.0.0.0`時，您可以從任何 Azure 資源存取 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器中的資料庫。 提供*name*參數的值，可協助您記住防火牆設定的用途。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫上的 **CONTROL** 權限。  
  
## <a name="examples"></a>範例  
 下列程式碼會建立稱為 `Allow Azure` 的資料庫層級防火牆設定，可讓您從 Azure 存取您的資料庫。  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 以下程式碼只會針對 IP 位址 `Example DB Setting 1` 建立名為 `0.0.0.4` 的資料庫層級防火牆設定。 然後，再次呼叫 `sp_set_database firewall_rule` 預存程式，將該防火牆設定中的結束 IP 位址更新為 `0.0.0.6`。 這會建立一個範圍，允許 `0.0.0.4`、`0.0.0.5`和 `0.0.0.6` 的 IP 位址存取資料庫。
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Azure SQL Database 防火牆](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [如何：設定防火牆設定（Azure SQL Database）](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;Azure SQL Database&#41; ](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;Azure SQL Database&#41; ](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [database_firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
