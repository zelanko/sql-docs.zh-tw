---
description: sp_setdefaultdatatypemapping (Transact-SQL)
title: sp_setdefaultdatatypemapping (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setdefaultdatatypemapping
- sp_setdefaultdatatypemapping_TSQL
helpviewer_keywords:
- sp_setdefaultdatatypemapping
ms.assetid: 7394e8ca-4ce1-4e99-a784-205007c2c248
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d31d4f44d7b1b60c527a5fa8abcf1e9736b1f674
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493021"
---
# <a name="sp_setdefaultdatatypemapping-transact-sql"></a>sp_setdefaultdatatypemapping (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將與非資料庫管理系統之間的現有資料類型對應標示 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 為預設 (DBMS) 。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_setdefaultdatatypemapping [ [ @mapping_id = ] mapping_id ]  
    [ , [ @source_dbms = ] 'source_dbms' ]  
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @source_length_min = ] source_length_min ]  
    [ , [ @source_length_max = ] source_length_max ]  
    [ , [ @source_precision_min = ] source_precision_min ]  
    [ , [ @source_precision_max = ] source_precision_max ]  
    [ , [ @source_scale_min = ] source_scale_min ]  
    [ , [ @source_scale_max = ] source_scale_max ]  
    [ , [ @source_nullable = ] source_nullable ]  
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @destination_length = ] destination_length ]  
    [ , [ @destination_precision = ] destination_precision ]  
    [ , [ @destination_scale = ] destination_scale ]  
    [ , [ @destination_nullable = ] source_nullable ]  
```  
  
## <a name="arguments"></a>引數  
`[ @mapping_id = ] mapping_id` 識別現有的資料類型對應。  *mapping_id* 是 **int**，預設值是 Null。 如果您指定 *mapping_id*，則不需要剩餘的參數。  
  
`[ @source_dbms = ] 'source_dbms'` 這是對應資料類型的來源 DBMS 名稱。 *source_dbms* 為 **sysname**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|來源是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**甲骨文**|來源是一個 Oracle 資料庫。|  
|NULL (預設值)||  
  
 如果 *mapping_id* 為 Null，您就必須指定這個參數。  
  
`[ @source_version = ] 'source_version'` 這是來源 DBMS 的版本號碼。 *source_version* 是 **Varchar (10) **，預設值是 Null。  
  
`[ @source_type = ] 'source_type'` 這是來源 DBMS 中的資料類型。 *source_type* 為 **sysname**。 如果 *mapping_id* 為 Null，您就必須指定這個參數。  
  
`[ @source_length_min = ] source_length_min` 這是來源 DBMS 中資料類型的最小長度。 *source_length_min* 是 **Bigint**，預設值是 Null。  
  
`[ @source_length_max = ] source_length_max` 這是來源 DBMS 中資料類型的最大長度。 *source_length_max* 是 **Bigint**，預設值是 Null。  
  
`[ @source_precision_min = ] source_precision_min` 這是來源 DBMS 中資料類型的最小有效位數。 *source_precision_min* 是 **Bigint**，預設值是 Null。  
  
`[ @source_precision_max = ] source_precision_max` 這是來源 DBMS 中資料類型的最大有效位數。 *source_precision_max* 是 **Bigint**，預設值是 Null。  
  
`[ @source_scale_min = ] source_scale_min` 這是來源 DBMS 中資料類型的最小小數位數。 *source_scale_min* 是 **int**，預設值是 Null。  
  
`[ @source_scale_max = ] source_scale_max` 這是來源 DBMS 中資料類型的最大刻度。 *source_scale_max* 是 **int**，預設值是 Null。  
  
`[ @source_nullable = ] source_nullable` 這是指來源 DBMS 中的資料類型是否支援 Null 值。 *source_nullable* 是 **bit**，預設值是 Null。 **1** 表示支援 Null 值。  
  
`[ @destination_dbms = ] 'destination_dbms'` 這是目的地 DBMS 的名稱。 *destination_dbms* 為 **sysname**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|目的地是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**甲骨文**|目的地是一個 Oracle 資料庫。|  
|**DB2**|目的地是一個 IBM DB2 資料庫。|  
|**Sybase**|目的地是一個 Sybase 資料庫。|  
|NULL (預設值)||  
  
`[ @destination_version = ] 'destination_version'` 這是目的地 DBMS 的產品版本。 *destination_version* 是 **Varchar (10) **，預設值是 Null。  
  
`[ @destination_type = ] 'destination_type'` 這是目的地 DBMS 中所列出的資料類型。 *destination_type* 是 **sysname**，預設值是 Null。  
  
`[ @destination_length = ] destination_length` 這是目的地 DBMS 中的資料類型長度。 *destination_length* 是 **Bigint**，預設值是 Null。  
  
`[ @destination_precision = ] destination_precision` 這是目的地 DBMS 中的資料類型有效位數。 *destination_precision* 是 **Bigint**，預設值是 Null。  
  
`[ @destination_scale = ] destination_scale` 這是目的地 DBMS 中的資料類型小數位數。 *destination_scale* 是 **int**，預設值是 Null。  
  
`[ @destination_nullable = ] destination_nullable` 這是指目的地 DBMS 中的資料類型是否支援 Null 值。 *destination_nullable* 是 **bit**，預設值是 Null。 **1** 表示支援 Null 值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_setdefaultdatatypemapping** 用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和非 DBMS 之間的所有複寫類型中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 預設資料類型對應套用至包含指定的 DBMS 之所有複寫拓撲。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_setdefaultdatatypemapping**。  
  
## <a name="see-also"></a>另請參閱  
 [指定 Oracle 發行者的資料類型對應](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [sp_getdefaultdatatypemapping &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
