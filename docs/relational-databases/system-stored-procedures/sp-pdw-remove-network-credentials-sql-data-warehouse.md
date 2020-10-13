---
description: 'sp_pdw_remove_network_credentials (SQL 資料倉儲) '
title: sp_pdw_remove_network_credentials
titleSuffix: Azure SQL Data Warehouse
ms.date: 03/14/2017
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.subservice: design
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.custom: seo-dt-2019
ms.openlocfilehash: 548779915a1d3a1753a99b16ac95969c755cbb19
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988774"
---
# <a name="sp_pdw_remove_network_credentials-sql-data-warehouse"></a>sp_pdw_remove_network_credentials (SQL 資料倉儲) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  這會移除儲存在中的網路認證 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ，以存取網路檔案共用。 例如，您可以使用這個預存程式來移除的許可權，以便 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 在位於您自己網路內的伺服器上執行備份和還原作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
## <a name="arguments"></a>引數  
 '*target_server_name*'  
 指定目標伺服器主機名稱或 IP 位址。 將會從移除存取此伺服器的認證 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。 這不會變更或移除您自己的小組所管理的實際目標伺服器上的任何許可權。  
  
 *target_server_name* 定義為 Nvarchar (337) 。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>權限  
 需要 **ALTER SERVER STATE** 許可權。  
  
## <a name="error-handling"></a>錯誤處理  
 如果在控制節點和所有計算節點上移除認證失敗，就會發生錯誤。  
  
## <a name="general-remarks"></a>一般備註  
 這個預存程式會從的 NetworkService 帳戶移除網路認證 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。 NetworkService 帳戶會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在控制節點和計算節點上執行 SMP 的每個實例。 例如，當備份作業執行時，控制節點和每個計算節點都會使用 NetworkService 帳號憑證來存取目標伺服器。  
  
## <a name="metadata"></a>中繼資料  
 若要列出所有認證並確認已移除認證，請使用 [sys.dm_pdw_network_credentials &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)。  
  
 若要新增認證，請使用 [sp_pdw_add_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)。  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>A. 移除用來執行資料庫備份的認證  
 下列範例會移除使用者名稱和密碼認證，以存取 IP 位址為10.192.147.63 的目標伺服器。  
  
```sql  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  

