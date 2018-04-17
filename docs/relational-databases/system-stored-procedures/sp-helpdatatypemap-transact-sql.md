---
title: sp_helpdatatypemap (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdatatypemap
- sp_helpdatatypemap_TSQL
helpviewer_keywords:
- sp_helpdatatypemap
ms.assetid: 800c9c65-723e-4961-a63d-327987f129f0
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e594c9b1d13730df2ccc93bf04d0348a5d2175b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回之間定義的資料類型對應的相關資訊[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和非-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫管理系統 (DBMS)。 這個預存程序執行於任何資料庫中的散發者端。  
  
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
 這是對應資料類型的來源 DBMS 名稱。 *source_dbms*是**sysname**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|來源是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**ORACLE**|來源是一個 Oracle 資料庫。|  
  
 [ **@source_version**=] **'***source_version***'**  
 這是來源 DBMS 的產品版本。 *source_version*是**varchar （10)**，如果未指定，資料類型會傳回的來源 DBMS 所有版本的對應。 啟用 DBMS 來源版本所要篩選的結果集。  
  
 [ **@source_type**=] **'***source_type***'**  
 這是來源 DBMS 中列出的資料類型。 *source_type*是**sysname**，如果未指定，會傳回來源 DBMS 中的所有資料類型對應。 啟用來源 DBMS 中的資料類型所要篩選的結果集。  
  
 [ **@destination_dbms** =] **'***destination_dbms***'**  
 這是目的地 DBMS 的名稱。 *destination_dbms*是**sysname**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|目的地是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**ORACLE**|目的地是一個 Oracle 資料庫。|  
|**DB2**|目的地是一個 IBM DB2 資料庫。|  
|**SYBASE**|目的地是一個 Sybase 資料庫。|  
  
 [ **@destination_version**=] **'***destination_version***'**  
 這是目的地 DBMS 的產品版本。 *destination_version*是**varchar （10)**，如果未指定，會傳回目的地 DBMS 所有版本的對應。 啟用 DBMS 目的地版本所要篩選的結果集。  
  
 [ **@destination_type**=] **'***destination_type***'**  
 這是目的地 DBMS 中列出的資料類型。 *destination_type*是**sysname**，如果未指定，會傳回目的地 DBMS 中的所有資料類型對應。 啟用目的地 DBMS 中的資料類型所要篩選的結果集。  
  
 [ **@defaults_only**=] *defaults_only*  
 這是指是否只傳回預設資料類型對應。 *defaults_only*是**元**，預設值是**0**。 **1**會傳回預設資料類型對應的方法。 **0**表示預設值，而且任何使用者定義資料類型對應傳回。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|Description|  
|-----------------|-----------------|  
|**mapping_id**|識別資料類型對應。|  
|**source_dbms**|這是來源 DBMS 的名稱和版本號碼。|  
|**source_type**|這是來源 DBMS 中的資料類型。|  
|**destination_dbms**|這是目的地 DBMS 的名稱。|  
|**destination_type**|這是目的地 DBMS 中的資料類型。|  
|**is_default**|這是指對應是預設對應或替代對應。 值為**0**表示此對應是使用者定義。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpdatatypemap**定義資料類型對應，從非 SQL Server 發行者和從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]非發行者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]「 訂閱者 」。  
  
 不支援指定的來源和目的地 DBMS 組合時， **sp_helpdatatypemap**傳回空的結果集。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色的成員的散發者**db_owner**散發資料庫上的固定的資料庫角色可以執行**sp_helpdatatypemap**.  
  
## <a name="see-also"></a>另請參閱  
 [sp_getdefaultdatatypemapping &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
