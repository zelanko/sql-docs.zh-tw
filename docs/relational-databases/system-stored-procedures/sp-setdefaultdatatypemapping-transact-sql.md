---
title: sp_setdefaultdatatypemapping (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9f0dfadc3b2b990d999df1d66069c4b68df9e6cf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104407"
---
# <a name="spsetdefaultdatatypemapping-transact-sql"></a>sp_setdefaultdatatypemapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將標記之間的現有資料類型對應[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫管理系統 (DBMS) 為預設值。 這個預存程序執行於任何資料庫中的散發者端。  
  
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
`[ @mapping_id = ] mapping_id` 識別現有的資料類型對應。  *mapping_id*已**int**，預設值是 NULL。 如果您指定*mapping_id*，則不需要的其他參數。  
  
`[ @source_dbms = ] 'source_dbms'` 是資料類型會對應來源 DBMS 的名稱。 *source_dbms*已**sysname**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|來源是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**ORACLE**|來源是一個 Oracle 資料庫。|  
|NULL (預設值)||  
  
 您必須指定這個參數，如果*mapping_id*是 NULL。  
  
`[ @source_version = ] 'source_version'` 是來源 DBMS 的版本號碼。 *source_version*已**varchar(10)** ，預設值是 NULL。  
  
`[ @source_type = ] 'source_type'` 是來源 DBMS 中的資料類型。 *source_type*已**sysname**。 您必須指定這個參數，如果*mapping_id*是 NULL。  
  
`[ @source_length_min = ] source_length_min` 是來源 DBMS 中的資料類型的最小長度。 *source_length_min*已**bigint**，預設值是 NULL。  
  
`[ @source_length_max = ] source_length_max` 是來源 DBMS 中的資料類型的最大長度。 *source_length_max*已**bigint**，預設值是 NULL。  
  
`[ @source_precision_min = ] source_precision_min` 這是來源 DBMS 中的資料類型最小有效位數。 *source_precision_min*已**bigint**，預設值是 NULL。  
  
`[ @source_precision_max = ] source_precision_max` 這是來源 DBMS 中的資料類型最大有效位數。 *source_precision_min*已**bigint**，預設值是 NULL。  
  
`[ @source_scale_min = ] source_scale_min` 是來源 DBMS 中的資料類型的最小縮放比例。 *source_scale_min*已**int**，預設值是 NULL。  
  
`[ @source_scale_max = ] source_scale_max` 是來源 DBMS 中的資料類型最大小數位數。 *source_scale_min*已**int**，預設值是 NULL。  
  
`[ @source_nullable = ] source_nullable` 這是來源 DBMS 中的資料型別是否支援 NULL 值。 *source_nullable*已**元**，預設值是 NULL。 **1**表示支援 NULL 值。  
  
`[ @destination_dbms = ] 'destination_dbms'` 是目的地 DBMS 的名稱。 *destination_dbms*已**sysname**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|目的地是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**ORACLE**|目的地是一個 Oracle 資料庫。|  
|**DB2**|目的地是一個 IBM DB2 資料庫。|  
|**SYBASE**|目的地是一個 Sybase 資料庫。|  
|NULL (預設值)||  
  
`[ @destination_version = ] 'destination_version'` 這是目的地 DBMS 的產品版本。 *destination_version*已**varchar(10)** ，預設值是 NULL。  
  
`[ @destination_type = ] 'destination_type'` 目的地 DBMS 中列出的資料類型。 *destination_type*已**sysname**，預設值是 NULL。  
  
`[ @destination_length = ] destination_length` 是目的地 DBMS 中的資料類型長度。 *destination_length*已**bigint**，預設值是 NULL。  
  
`[ @destination_precision = ] destination_precision` 這是目的地 DBMS 中的資料類型有效位數。 *destination_precision*已**bigint**，預設值是 NULL。  
  
`[ @destination_scale = ] destination_scale` 是目的地 DBMS 中的資料類型的小數位數。 *destination_scale*已**int**，預設值是 NULL。  
  
`[ @destination_nullable = ] destination_nullable` 這是目的地 DBMS 中的資料類型是否支援 NULL 值。 *destination_nullable*已**元**，預設值是 NULL。 **1**表示支援 NULL 值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_setdefaultdatatypemapping**用於所有類型之間的複寫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBMS。  
  
 預設資料類型對應套用至包含指定的 DBMS 之所有複寫拓撲。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_setdefaultdatatypemapping**。  
  
## <a name="see-also"></a>另請參閱  
 [指定 「 Oracle 發行者 」 端的資料類型對應](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [sp_getdefaultdatatypemapping &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
