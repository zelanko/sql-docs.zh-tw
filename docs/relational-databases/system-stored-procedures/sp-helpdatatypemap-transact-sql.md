---
title: sp_helpdatatypemap （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 0b9666c13a2e4d8183d19fade64bf49b13377b9a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771065"
---
# <a name="sp_helpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  傳回和非[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫管理系統（DBMS）之間定義之資料類型對應的資訊。 這個預存程序執行於任何資料庫中的散發者端。  
  
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
`[ @source_dbms = ] 'source_dbms'`這是對應資料類型的來源 DBMS 名稱。 *source_dbms*是**sysname**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|來源是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**ORACLE**|來源是一個 Oracle 資料庫。|  
  
`[ @source_version = ] 'source_version'`這是來源 DBMS 的產品版本。 *source_version*為**Varchar （10）**，如果未指定，則會傳回來源 DBMS 所有版本的資料類型對應。 啟用 DBMS 來源版本所要篩選的結果集。  
  
`[ @source_type = ] 'source_type'`這是來源 DBMS 中列出的資料類型。 *source_type*是**sysname**，如果未指定，則會傳回來源 DBMS 中所有資料類型的對應。 啟用來源 DBMS 中的資料類型所要篩選的結果集。  
  
`[ @destination_dbms = ] 'destination_dbms'`這是目的地 DBMS 的名稱。 *destination_dbms*是**sysname**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|目的地是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。|  
|**ORACLE**|目的地是一個 Oracle 資料庫。|  
|**DB2**|目的地是一個 IBM DB2 資料庫。|  
|**所在**|目的地是一個 Sybase 資料庫。|  
  
`[ @destination_version = ] 'destination_version'`這是目的地 DBMS 的產品版本。 *destination_version*為**Varchar （10）**，如果未指定，則會傳回目的地 DBMS 所有版本的對應。 啟用 DBMS 目的地版本所要篩選的結果集。  
  
`[ @destination_type = ] 'destination_type'`這是目的地 DBMS 中所列出的資料類型。 *destination_type*是**sysname**，如果未指定，則會傳回目的地 DBMS 中所有資料類型的對應。 啟用目的地 DBMS 中的資料類型所要篩選的結果集。  
  
`[ @defaults_only = ] defaults_only`這是指是否只傳回預設資料類型對應。 *defaults_only*是**bit**，預設值是**0**。 **1**表示只傳回預設資料類型對應。 **0**表示會傳回預設值和任何使用者定義的資料類型對應。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|**mapping_id**|識別資料類型對應。|  
|**source_dbms**|這是來源 DBMS 的名稱和版本號碼。|  
|**source_type**|這是來源 DBMS 中的資料類型。|  
|**destination_dbms**|這是目的地 DBMS 的名稱。|  
|**destination_type**|這是目的地 DBMS 中的資料類型。|  
|**is_default**|這是指對應是預設對應或替代對應。 值為**0**表示這個對應是使用者定義的。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpdatatypemap**會定義從非 SQL Server 發行者和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者到非「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者」的資料類型對應。  
  
 當不支援指定的來源和目的地 DBMS 組合時， **sp_helpdatatypemap**會傳回空的結果集。  
  
## <a name="permissions"></a>權限  
 只有在散發者端的**系統管理員（sysadmin** ）固定伺服器角色成員，或散發資料庫上之**db_owner**固定資料庫角色的成員，才能夠執行**sp_helpdatatypemap**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_getdefaultdatatypemapping &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
