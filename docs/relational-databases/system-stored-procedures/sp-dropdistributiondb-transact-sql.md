---
title: sp_dropdistributiondb (Transact-sql) |Microsoft Docs
description: 卸載散發資料庫和其所使用的檔案（如果沒有其他資料庫使用的話）。 這個預存程式會在任何資料庫的散發者端執行。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistributiondb_TSQL
- sp_dropdistributiondb
helpviewer_keywords:
- sp_dropdistributiondb
ms.assetid: b6dd1846-2259-4d29-93af-a70a5d25a0c5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d5c1cb17767cf61b49345b93f7c5ee5ebfbc9d27
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543462"
---
# <a name="sp_dropdistributiondb-transact-sql"></a>sp_dropdistributiondb (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  卸除散發資料庫。 如果資料庫所用的實體檔案沒有另一個資料庫在使用，便卸除這些實體檔案。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropdistributiondb [ @database= ] 'database'  
```  
  
## <a name="arguments"></a>引數  
`[ @database = ] 'database'` 這是要卸載的資料庫。 *資料庫* 是 **sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_dropdistributiondb** 用於所有類型的複寫中。  
  
 執行 **sp_dropdistributor**之前，必須先執行這個預存程式，然後再卸載散發者。  
  
 **sp_dropdistributiondb** 也會移除散發資料庫的佇列讀取器代理程式作業（如果有的話）。  
  
 若要停用散發，散發資料庫必須在線上。 如果散發資料庫的資料庫快照集存在，您必須先卸除它，才能停用散發。 資料庫快照集是資料庫的唯讀離線複本，與複寫快照集無關。 如需詳細資訊，請參閱[資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributiondb-tr_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_dropdistributiondb**。  
  
## <a name="see-also"></a>另請參閱  
 [停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistributiondb &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
