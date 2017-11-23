---
title: "sp_db_increased_partitions |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_db_increased_partitions_TSQL
- sp_db_increased_partitions
dev_langs: TSQL
helpviewer_keywords: sp_db_increased_partitions
ms.assetid: a8c043ec-b504-4929-ac0e-8babaa99d989
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5266ce8c25465b6fd398111e7fd7e2d6634f5f34
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spdbincreasedpartitions"></a>sp_db_increased_partitions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  啟用或停止對於指定資料庫之 15,000 個資料分割上限的支援。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
||  
|-|  
|**適用於**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2 至[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]SP1 和更新版本)。 如需詳細資訊，請參閱[支援 15,000 個資料分割，在 SQL Server 2008 SP2 和 SQL Server 2008 R2 SP1](http://go.microsoft.com/fwlink/p/?LinkId=299658)，|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>引數  
 [ @dbname=] '*database_name*'  
 這是資料庫的名稱。 *dbname*是**sysname**預設值是 NULL。 如果*dbname*未指定，會使用目前的資料庫。  
  
 [ @increased_partitions=] '*increased_partitions*'  
 啟用或停止對於指定資料庫之 15,000 個資料分割上限的支援。 *increased_partitions*是**varchar(6)**預設值是 NULL。 接受的值如果是 'ON' 或 'TRUE'，表示啟用支援，如果是 'OFF' 或 'FALSE'，即表示停用支援。 如果*increased_partitions*未指定，此程序會傳回 1，指出指定的資料庫已啟用支援，或 0，表示支援已停用。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>Permissions  
 需要指定資料庫的 ALTER DATABASE 權限。  
  
  
