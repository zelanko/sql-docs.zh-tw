---
description: sp_getdefaultdatatypemapping (Transact-SQL)
title: sp_getdefaultdatatypemapping (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getdefaultdatatypemapping_TSQL
- sp_getdefaultdatatypemapping
helpviewer_keywords:
- sp_getdefaultdatatypemapping
ms.assetid: b8401de1-f135-41d0-ba79-ce8fe1f48c00
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6bbd01e86f8b5cfbc24a04dee1482ddb4652354f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469418"
---
# <a name="sp_getdefaultdatatypemapping-transact-sql"></a>sp_getdefaultdatatypemapping (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫管理系統 (DBMS) 之間，指定之資料類型的預設對應相關資訊。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_getdefaultdatatypemapping [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
        , [ @source_type = ] 'source_type'    
    [ , [ @source_length = ] source_length ]  
    [ , [ @source_precision = ] source_precision ]  
    [ , [ @source_scale = ] source_scale ]  
    [ , [ @source_nullable = ] source_nullable ]  
        , [ @destination_dbms = ] 'destination_dbms'   
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' OUTPUT ]  
    [ , [ @destination_length = ] destination_length OUTPUT ]  
    [ , [ @destination_precision = ] destination_precision OUTPUT ]  
    [ , [ @destination_scale = ] destination_scale OUTPUT ]  
    [ , [ @destination_nullable = ] source_nullable OUTPUT ]  
    [ , [ @dataloss = ] dataloss OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
`[ @source_dbms = ] 'source_dbms'` 這是對應資料類型的來源 DBMS 名稱。 *source_dbms* 為 **sysname**，而且可以是下列其中一個值：  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|來源是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**甲骨文**|來源是一個 Oracle 資料庫。|  
  
 您必須指定這個參數。  
  
`[ @source_version = ] 'source_version'` 這是來源 DBMS 的版本號碼。 *source_version* 是 **Varchar (10) **，預設值是 Null。  
  
`[ @source_type = ] 'source_type'` 這是來源 DBMS 中的資料類型。 *source_type* 是 **sysname**，沒有預設值。  
  
`[ @source_length = ] source_length` 這是來源 DBMS 中的資料類型長度。 *source_length* 是 **Bigint**，預設值是 Null。  
  
`[ @source_precision = ] source_precision` 這是來源 DBMS 中資料類型的有效位數。 *source_precision* 是 **Bigint**，預設值是 Null。  
  
`[ @source_scale = ] source_scale` 這是來源 DBMS 中資料類型的小數位數。 *source_scale* 是 **int**，預設值是 Null。  
  
`[ @source_nullable = ] source_nullable` 這是指來源 DBMS 中的資料類型是否支援 Null 值。 *source_nullable* 是 **bit**，預設值是 **1**，表示支援 Null 值。  
  
`[ @destination_dbms = ] 'destination_dbms'` 這是目的地 DBMS 的名稱。 *destination_dbms* 為 **sysname**，而且可以是下列其中一個值：  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|目的地是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**甲骨文**|目的地是一個 Oracle 資料庫。|  
|**DB2**|目的地是一個 IBM DB2 資料庫。|  
|**Sybase**|目的地是一個 Sybase 資料庫。|  
  
 您必須指定這個參數。  
  
`[ @destination_version = ] 'destination_version'` 這是目的地 DBMS 的產品版本。 *destination_version* 是 **Varchar (10) **，預設值是 Null。  
  
`[ @destination_type = ] 'destination_type' OUTPUT` 這是目的地 DBMS 中所列出的資料類型。 *destination_type* 是 **sysname**，預設值是 Null。  
  
`[ @destination_length = ] destination_length OUTPUT` 這是目的地 DBMS 中的資料類型長度。 *destination_length* 是 **Bigint**，預設值是 Null。  
  
`[ @destination_precision = ] destination_precision OUTPUT` 這是目的地 DBMS 中的資料類型有效位數。 *destination_precision* 是 **Bigint**，預設值是 Null。  
  
`[ @destination_scale = ] _destination_scaleOUTPUT` 這是目的地 DBMS 中的資料類型小數位數。 *destination_scale* 是 **int**，預設值是 Null。  
  
`[ @destination_nullable = ] _destination_nullableOUTPUT` 這是指目的地 DBMS 中的資料類型是否支援 Null 值。 *destination_nullable* 是 **bit**，預設值是 Null。 **1** 表示支援 Null 值。  
  
`[ @dataloss = ] _datalossOUTPUT` 這是指對應是否可能遺失資料。 *資料遺失* 是 **bit**，預設值是 Null。 **1** 表示可能遺失資料。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_getdefaultdatatypemapping** 用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和非 DBMS 之間的所有複寫類型中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **sp_getdefaultdatatypemapping** 傳回最符合指定之源資料類型的預設目的地資料類型。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_getdefaultdatatypemapping**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_helpdatatypemap &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md)  
  
  
