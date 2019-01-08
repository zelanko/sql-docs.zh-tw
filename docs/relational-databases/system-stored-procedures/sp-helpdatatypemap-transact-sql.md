---
title: sp_helpdatatypemap (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdatatypemap
- sp_helpdatatypemap_TSQL
helpviewer_keywords:
- sp_helpdatatypemap
ms.assetid: 800c9c65-723e-4961-a63d-327987f129f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c1d4addec6f0b5a7faff69d513c655450202d099
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210847"
---
# <a name="sphelpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回之間所定義的資料類型對應的相關資訊[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和非-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫管理系統 (DBMS)。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpdatatypemap [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @defaults_only = ] defaults_only ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@source_dbms**=] **'***source_dbms***'**  
 這是對應資料類型的來源 DBMS 名稱。 *source_dbms*已**sysname**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|來源是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**ORACLE**|來源是一個 Oracle 資料庫。|  
  
 [ **@source_version**=] **'***source_version***'**  
 這是來源 DBMS 的產品版本。 *source_version*已**varchar(10)**，如果未指定，資料類型會傳回的來源 DBMS 所有版本的對應。 啟用 DBMS 來源版本所要篩選的結果集。  
  
 [ **@source_type**=] **'***source_type***'**  
 這是來源 DBMS 中列出的資料類型。 *source_type*已**sysname**，如果未指定，會傳回來源 DBMS 中的所有資料類型的對應。 啟用來源 DBMS 中的資料類型所要篩選的結果集。  
  
 [ **@destination_dbms** =] **'***destination_dbms***'**  
 這是目的地 DBMS 的名稱。 *destination_dbms*已**sysname**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|目的地是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**ORACLE**|目的地是一個 Oracle 資料庫。|  
|**DB2**|目的地是一個 IBM DB2 資料庫。|  
|**SYBASE**|目的地是一個 Sybase 資料庫。|  
  
 [ **@destination_version**=] **'***destination_version***'**  
 這是目的地 DBMS 的產品版本。 *destination_version*已**varchar(10)**，如果未指定，會傳回目的地 DBMS 所有版本的對應。 啟用 DBMS 目的地版本所要篩選的結果集。  
  
 [ **@destination_type**=] **'***destination_type***'**  
 這是目的地 DBMS 中列出的資料類型。 *destination_type*已**sysname**，如果未指定，會傳回目的地 DBMS 中的所有資料類型的對應。 啟用目的地 DBMS 中的資料類型所要篩選的結果集。  
  
 [ **@defaults_only**=] *defaults_only*  
 這是指是否只傳回預設資料類型對應。 *defaults_only*已**位元**，預設值是**0**。 **1**會傳回預設資料類型對應的方法。 **0**會傳回預設值，而且任何使用者定義資料類型對應的方法。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|**mapping_id**|識別資料類型對應。|  
|**source_dbms**|這是來源 DBMS 的名稱和版本號碼。|  
|**source_type**|這是來源 DBMS 中的資料類型。|  
|**destination_dbms**|這是目的地 DBMS 的名稱。|  
|**destination_type**|這是目的地 DBMS 中的資料類型。|  
|**is_default**|這是指對應是預設對應或替代對應。 值為**0**表示這個對應是由使用者定義。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpdatatypemap**定義從非 SQL Server 發行者和從資料類型對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者。  
  
 不支援指定的來源和目的地 DBMS 組合時， **sp_helpdatatypemap**傳回空的結果集。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色的成員的散發者端**db_owner**散發資料庫的固定的資料庫角色可以執行**sp_helpdatatypemap**.  
  
## <a name="see-also"></a>另請參閱  
 [sp_getdefaultdatatypemapping &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
