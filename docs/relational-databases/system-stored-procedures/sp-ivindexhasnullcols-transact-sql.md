---
title: "sp_ivindexhasnullcols (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3dbdbe2a627eb49dbd2ab71bef5bc102f1b157d7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  驗證索引檢視的叢集索引是唯一的，且並未包含將利用索引檢視來建立交易式發行集時，可為 Null 值的任何資料行。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>引數  
 [  **@viewname** =] **'***view_name***'**  
 這是要驗證的檢視名稱。 *view_name*是**sysname**，沒有預設值。  
  
 [  **@fhasnullcols** =] *field_has_null_columns*輸出  
 這是一個旗標，用來指示檢視索引是否有允許 NULL 的資料行。 *view_name*是**sysname**，沒有預設值。 傳回值的**1**檢視索引是否允許 NULL 的資料行。 傳回值的**0**如果檢視不包含允許 null 值的資料行。  
  
> [!NOTE]  
>  如果預存程序本身傳回的傳回碼**1**，這表示預存程序執行失敗，這個值是**0** ，應予忽略。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_ivindexhasnullcols**正由異動複寫。  
  
 依預設，發行集中的索引檢視發行項會建立成訂閱者端的資料表。 不過，當索引資料行允許 NULL 值時，會將索引檢視建立成在訂閱者端的索引檢視，而非資料表。 當執行這個預存程序時，它可以警示使用者目前的索引檢視有沒有這個問題。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_ivindexhasnullcols**。  
  
## <a name="see-also"></a>請參閱＜  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
