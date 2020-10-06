---
description: 'sp_pdw_add_network_credentials (SQL 資料倉儲) '
title: sp_pdw_add_network_credentials
titleSuffix: Azure SQL Data Warehouse
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0729eeff-ac7e-43f0-80fa-ff5346a75985
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.custom: seo-dt-2019
ms.openlocfilehash: d4fea3d262eea3e4e329809137720e94a7af5d93
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724049"
---
# <a name="sp_pdw_add_network_credentials-sql-data-warehouse"></a>sp_pdw_add_network_credentials (SQL 資料倉儲) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  這會將網路認證儲存在中 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ，並將它們與伺服器產生關聯。 例如，您可以使用這個預存程式來授與 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 適當的讀取/寫入權限，以便在目標伺服器上執行資料庫備份和還原作業，或建立用於 TDE 的憑證備份。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_add_network_credentials 'target_server_name',  'user_name', ꞌpasswordꞌ  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="arguments"></a>引數  
 '*target_server_name*'  
 指定目標伺服器主機名稱或 IP 位址。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 將使用傳遞至此預存程式的使用者名稱和密碼認證來存取此伺服器。  
  
 若要透過「不會」網路進行連線，請使用目標伺服器的 [不限] IP 位址。  
  
 *target_server_name* 定義為 Nvarchar (337) 。  
  
 '*user_name*'  
 指定擁有存取目標伺服器之許可權的 user_name。 如果目標伺服器的認證已存在，則會將其更新為新的認證。  
  
 *user_name* 定義為 Nvarchar (513) 。  
  
 '*密碼*ꞌ  
 指定 *user_name*的密碼。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>權限  
 需要 **ALTER SERVER STATE** 許可權。  
  
## <a name="error-handling"></a>錯誤處理  
 如果在控制項節點和所有計算節點上新增認證失敗，就會發生錯誤。  
  
## <a name="general-remarks"></a>一般備註  
 這個預存程式會將網路認證新增至的 NetworkService 帳戶 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。 NetworkService 帳戶會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在控制節點和計算節點上執行 SMP 的每個實例。 例如，當備份作業執行時，控制節點和每個計算節點都會使用 NetworkService 帳號憑證來取得目標伺服器的讀取和寫入權限。  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-add-credentials-for-performing-a-database-backup"></a>A. 新增用來執行資料庫備份的認證  
 下列範例會將網域使用者 seattle\david 的使用者名稱和密碼認證，與 IP 位址為10.172.63.255 的目標伺服器產生關聯。 使用者 seattle\david 具有目標伺服器的讀取/寫入權限。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 會儲存這些認證，並視備份和還原作業的需要，使用這些認證來讀取和寫入目標伺服器。  
  
```sql  
EXEC sp_pdw_add_network_credentials '10.172.63.255', 'seattle\david', '********';  
```  
  
 Backup 命令需要以 IP 位址的形式輸入伺服器名稱。  
  
> [!NOTE]  
>  若要透過自動程式執行資料庫備份，請務必使用備份伺服器的「不會」 IP 位址。  
  
## <a name="see-also"></a>另請參閱  
 [sp_pdw_remove_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
  

