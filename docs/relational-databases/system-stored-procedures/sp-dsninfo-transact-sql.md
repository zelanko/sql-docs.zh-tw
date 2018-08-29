---
title: sp_dsninfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_dsninfo
- sp_dsninfo_TSQL
helpviewer_keywords:
- sp_dsninfo
ms.assetid: 34648615-814b-42bc-95a3-50e86b42ec4d
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 63e4783420f9298e2e820341993774b81bbab7e3
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43017491"
---
# <a name="spdsninfo-transact-sql"></a>sp_dsninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [  **@dsn =**] **'***dsn***'**  
 這是 ODBC DSN 或 OLE DB 連結伺服器的名稱。 *dsn*已**varchar(128)**，沒有預設值。  
  
 [  **@infotype =**] **'***info_type***'**  
 這是要傳回的資訊類型。 如果*info_type*未指定或指定 NULL，則會傳回所有資訊類型。 *info_type*已**varchar(128)**，預設值是 NULL，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**DBMS_NAME**|指定資料來源供應商名稱。|  
|**DBMS_VERSION**|指定資料來源版本。|  
|**DATABASE_NAME**|指定資料庫名稱。|  
|**SQL_SUBSCRIBER**|指定資料來源可以是訂閱者。|  
  
 [  **@login =**] **'***登入***'**  
 這是資料來源的登入。 如果資料來源包括登入，請指定 NULL 或省略這個參數。 *登入*已**varchar(128)**，預設值是 NULL。  
  
 [  **@password =**] **'***密碼***'**  
 這是登入的密碼。 如果資料來源包括登入，請指定 NULL 或省略這個參數。 *密碼*已**varchar(128)**，預設值是 NULL。  
  
 [  **@dso_type=**] *dso_type*  
 這是資料來源類型。 *dso_type*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1** (預設值)|ODBC 資料來源|  
|**3**|OLE DB 資料來源|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**資訊類型**|**nvarchar(64)**|資訊類型，例如 DBMS_NAME、DBMS_VERSION、DATABASE_NAME、SQL_SUBSCRIBER。|  
|**值**|**nvarchar(512)**|相關資訊類型的值。|  
  
## <a name="remarks"></a>備註  
 **sp_dsninfo**用於所有類型的複寫。  
  
 **sp_dsninfo**擷取 ODBC 或 OLE DB 的資料來源資訊會顯示資料庫是否可用於複寫或查詢。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_dsninfo**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_enumdsn &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-enumdsn-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
