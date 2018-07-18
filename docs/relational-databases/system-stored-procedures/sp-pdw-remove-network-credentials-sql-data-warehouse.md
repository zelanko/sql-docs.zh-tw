---
title: sp_pdw_remove_network_credentials （SQL 資料倉儲） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: system-objects
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: c12696a2-5939-402b-9866-8a837ca4c0a3
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c44633ebcfb79b433a7420055343faf36774da39
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37989280"
---
# <a name="sppdwremovenetworkcredentials-sql-data-warehouse"></a>sp_pdw_remove_network_credentials （SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  這會移除網路認證儲存在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]存取網路檔案共用。 例如，若要移除的權限使用這個預存程序[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]執行備份和還原位於自己的網路中的伺服器上的作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_remove_network_credentials 'target_server_name'  
```  
  
## <a name="arguments"></a>引數  
 '*target_server_name*'  
 指定的目標伺服器主機名稱或 IP 位址。 若要存取此伺服器的認證將會移除從[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 這不會變更或移除其受您自己的小組在實際的目標伺服器上的任何權限。  
  
 *target_server_name*定義為 nvarchar(337)。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>Permissions  
 需要**ALTER SERVER STATE**權限。  
  
## <a name="error-handling"></a>錯誤處理  
 如果移除認證不成功的控制節點和所有計算節點上，就會發生錯誤。  
  
## <a name="general-remarks"></a>一般備註  
 這個預存程序會移除的 NetworkService 帳戶中的網路認證[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 NetworkService 帳戶執行每個執行個體的 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]控制節點和計算節點上。 比方說，當備份作業執行時，控制節點和每個計算節點，將會存取目標伺服器來使用 NetworkService 帳戶認證。  
  
## <a name="metadata"></a>中繼資料  
 若要列出所有認證，並確認已移除認證，請使用[sys.dm_pdw_network_credentials &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)。  
  
 若要新增認證，請使用[sp_pdw_add_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-remove-credentials-for-performing-a-database-backup"></a>A. 移除認證來執行資料庫備份  
 下列範例會移除存取 10.192.147.63 IP 位址的目標伺服器的使用者名稱和密碼認證。  
  
```  
EXEC sp_pdw_remove_network_credentials '10.192.147.63';  
```  
  
  

