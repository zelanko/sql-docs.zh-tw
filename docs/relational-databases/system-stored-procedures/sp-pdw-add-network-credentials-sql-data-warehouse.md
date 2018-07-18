---
title: sp_pdw_add_network_credentials （SQL 資料倉儲） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0729eeff-ac7e-43f0-80fa-ff5346a75985
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7f2dfe569a163b7a8268f925a5f48849778b3454
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052256"
---
# <a name="sppdwaddnetworkcredentials-sql-data-warehouse"></a>sp_pdw_add_network_credentials （SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  這會儲存在 網路認證[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]並將它們與伺服器相關聯。 比方說，使用此預存程序提供[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]適當的讀取/寫入權限來執行資料庫備份和還原作業的目標伺服器上，或建立一份用於 TDE 的憑證。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_add_network_credentials 'target_server_name',  'user_name', ꞌpasswordꞌ  
```  
  
## <a name="arguments"></a>引數  
 '*target_server_name*'  
 指定的目標伺服器主機名稱或 IP 位址。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 會使用傳遞給這個預存程序的使用者名稱和密碼認證來存取此伺服器。  
  
 若要透過 InfiniBand 網路連線，使用目標伺服器的 InfiniBand IP 位址。  
  
 *target_server_name*定義為 nvarchar(337)。  
  
 '*user_name*'  
 指定具有存取目標伺服器的權限的使用者名稱。 如果認證已存在目標伺服器，它們將會更新至新的認證。  
  
 *user_name*定義為 nvarchar (513)。  
  
 '*密碼*ꞌ  
 指定的密碼*user_name*。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>Permissions  
 需要**ALTER SERVER STATE**權限。  
  
## <a name="error-handling"></a>錯誤處理  
 如果將認證加入控制節點和所有計算節點上未成功，就會發生錯誤。  
  
## <a name="general-remarks"></a>一般備註  
 這個預存程序會將的 NetworkService 帳戶中的網路認證[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 NetworkService 帳戶執行每個執行個體的 SMP[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]控制節點和計算節點上。 比方說，當備份作業執行時，控制節點和每個計算節點，會取得讀取和寫入到目標伺服器的權限來使用 NetworkService 帳戶認證。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-add-credentials-for-performing-a-database-backup"></a>A. 新增認證執行資料庫備份  
 下列範例會將網域使用者 seattle\david 的使用者名稱和密碼認證關聯的目標伺服器，10.172.63.255 IP 位址。 使用者 seattle\david 具有讀取/寫入權限給目標伺服器。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 將會儲存這些認證，並使用它們來讀取和寫入與目標伺服器，視您的備份和還原作業。  
  
```  
EXEC sp_pdw_add_network_credentials '10.172.63.255', 'seattle\david', '********';  
```  
  
 備份命令需要伺服器名稱以輸入 IP 位址。  
  
> [!NOTE]  
>  若要執行的資料庫備份，透過 InfiniBand，務必要使用備份伺服器的 InfiniBand IP 位址。  
  
## <a name="see-also"></a>另請參閱  
 [sp_pdw_remove_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
  

