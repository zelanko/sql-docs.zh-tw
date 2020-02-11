---
title: sp_getdefaultdatatypemapping （Transact-sql） |Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 32fe9edf5c3d8621046a27937d83f642b1689d1a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68123994"
---
# <a name="sp_getdefaultdatatypemapping-transact-sql"></a>sp_getdefaultdatatypemapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對和非[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫管理系統（DBMS）之間的指定資料類型，傳回預設對應的相關資訊。 這個預存程序執行於任何資料庫中的散發者端。  
  
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
`[ @source_dbms = ] 'source_dbms'`這是對應資料類型的來源 DBMS 名稱。 *source_dbms*是**sysname**，而且可以是下列其中一個值：  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|來源是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**ORACLE**|來源是一個 Oracle 資料庫。|  
  
 您必須指定這個參數。  
  
`[ @source_version = ] 'source_version'`這是來源 DBMS 的版本號碼。 *source_version*是**Varchar （10）**，預設值是 Null。  
  
`[ @source_type = ] 'source_type'`這是來源 DBMS 中的資料類型。 *source_type*是**sysname**，沒有預設值。  
  
`[ @source_length = ] source_length`這是來源 DBMS 中的資料類型長度。 *source_length*是**Bigint**，預設值是 Null。  
  
`[ @source_precision = ] source_precision`這是來源 DBMS 中資料類型的有效位數。 *source_precision*是**Bigint**，預設值是 Null。  
  
`[ @source_scale = ] source_scale`這是來源 DBMS 中資料類型的小數值。 *source_scale*是**int**，預設值是 Null。  
  
`[ @source_nullable = ] source_nullable`這是指來源 DBMS 中的資料類型是否支援 Null 值。 *source_nullable*是**bit**，預設值是**1**，表示支援 Null 值。  
  
`[ @destination_dbms = ] 'destination_dbms'`這是目的地 DBMS 的名稱。 *destination_dbms*是**sysname**，而且可以是下列其中一個值：  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|目的地是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**ORACLE**|目的地是一個 Oracle 資料庫。|  
|**DB2**|目的地是一個 IBM DB2 資料庫。|  
|**所在**|目的地是一個 Sybase 資料庫。|  
  
 您必須指定這個參數。  
  
`[ @destination_version = ] 'destination_version'`這是目的地 DBMS 的產品版本。 *destination_version*是**Varchar （10）**，預設值是 Null。  
  
`[ @destination_type = ] 'destination_type' OUTPUT`這是目的地 DBMS 中所列出的資料類型。 *destination_type*是**sysname**，預設值是 Null。  
  
`[ @destination_length = ] destination_length OUTPUT`這是目的地 DBMS 中的資料類型長度。 *destination_length*是**Bigint**，預設值是 Null。  
  
`[ @destination_precision = ] destination_precision OUTPUT`這是目的地 DBMS 中資料類型的有效位數。 *destination_precision*是**Bigint**，預設值是 Null。  
  
`[ @destination_scale = ] _destination_scaleOUTPUT`這是目的地 DBMS 中資料類型的小數值。 *destination_scale*是**int**，預設值是 Null。  
  
`[ @destination_nullable = ] _destination_nullableOUTPUT`這是指目的地 DBMS 中的資料類型是否支援 Null 值。 *destination_nullable*是**bit**，預設值是 Null。 **1**表示支援 Null 值。  
  
`[ @dataloss = ] _datalossOUTPUT`這是指對應是否可能遺失資料。 *資料遺失*是**bit**，預設值是 Null。 **1**表示可能會遺失資料。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_getdefaultdatatypemapping**用於和非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBMS 之間的所有複寫類型中。  
  
 **sp_getdefaultdatatypemapping**會傳回與指定之源資料類型最相符的預設目的地資料類型。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_getdefaultdatatypemapping**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_helpdatatypemap &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [IBM DB2 訂閱者](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle 訂閱者](../../relational-databases/replication/non-sql/oracle-subscribers.md)  
  
  
