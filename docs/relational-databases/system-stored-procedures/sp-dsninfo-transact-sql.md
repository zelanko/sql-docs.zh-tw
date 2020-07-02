---
title: sp_dsninfo （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dsninfo
- sp_dsninfo_TSQL
helpviewer_keywords:
- sp_dsninfo
ms.assetid: 34648615-814b-42bc-95a3-50e86b42ec4d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d7409d28b6a21a033c139c63ca6d6e7524e6ba50
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783769"
---
# <a name="sp_dsninfo-transact-sql"></a>sp_dsninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  從目前伺服器相關聯的散發者傳回 ODBC 或 OLE DB 資料來源資訊。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dsninfo [ @dsn =] 'dsn'   
    [ , [ @infotype =] 'info_type']   
    [ , [ @login =] 'login']   
    [ , [ @password =] 'password']  
    [ , [ @dso_type=] dso_type]  
```  
  
## <a name="arguments"></a>引數  
`[ @dsn = ] 'dsn'`這是 ODBC DSN 或 OLE DB 連結伺服器的名稱。 *dsn*是**Varchar （128）**，沒有預設值。  
  
`[ @infotype = ] 'info_type'`這是要傳回的資訊類型。 如果未指定*info_type* ，或指定了 Null，則會傳回所有資訊類型。 *info_type*是**Varchar （128）**，預設值是 Null，它可以是下列值之一。  
  
|值|說明|  
|-----------|-----------------|  
|**DBMS_NAME**|指定資料來源供應商名稱。|  
|**DBMS_VERSION**|指定資料來源版本。|  
|**DATABASE_NAME**|指定資料庫名稱。|  
|**SQL_SUBSCRIBER**|指定資料來源可以是訂閱者。|  
  
`[ @login = ] 'login'`這是資料來源的登入。 如果資料來源包括登入，請指定 NULL 或省略這個參數。 *login*是**Varchar （128）**，預設值是 Null。  
  
`[ @password = ] 'password'`這是登入的密碼。 如果資料來源包括登入，請指定 NULL 或省略這個參數。 *password*是**Varchar （128）**，預設值是 Null。  
  
`[ @dso_type = ] dso_type`這是資料來源類型。 *dso_type*是**int**，而且可以是下列其中一個值。  
  
|值|說明|  
|-----------|-----------------|  
|**1** (預設值)|ODBC 資料來源|  
|**3**|OLE DB 資料來源|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**資訊類型**|**Nvarchar （64）**|資訊類型，例如 DBMS_NAME、DBMS_VERSION、DATABASE_NAME、SQL_SUBSCRIBER。|  
|**ReplTest1**|**nvarchar(512)**|相關資訊類型的值。|  
  
## <a name="remarks"></a>備註  
 **sp_dsninfo**用於所有類型的複寫中。  
  
 **sp_dsninfo**會抓取 ODBC 或 OLE DB 資料來源資訊，以顯示資料庫是否可以用於複寫或查詢。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_dsninfo**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_enumdsn &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
