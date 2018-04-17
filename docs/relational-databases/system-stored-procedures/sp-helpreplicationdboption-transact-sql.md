---
title: sp_helpreplicationdboption (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
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
- sp_helpreplicationdboption_TSQL
- sp_helpreplicationdboption
helpviewer_keywords:
- sp_helpreplicationdboption
ms.assetid: 143ce689-108b-49d7-9892-fd3a86897f38
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 050eb8a82a7c4e9b3204af812072ea83fec7ecea
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpreplicationdboption-transact-sql"></a>sp_helpreplicationdboption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示發行者端的資料庫是否啟用複寫。 這個預存程序執行於任何資料庫的發行者端。 *不支援 Oracle 發行者。*  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpreplicationdboption [ [ @dbname =] 'dbname' ]  
    [ , [ @type = ] 'type' ]  
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@dbname=**] **'***dbname***'**  
 這是資料庫的名稱。 *dbname*是**sysname**，預設值是**%**。 如果**%**，則結果集包含在 「 發行者 」 的所有資料庫，否則為指定的資料庫上的唯一資訊會傳回。 如下所描述，使用者沒有適當權限的任何資料庫都不會傳回資訊。  
  
 [  **@type=**] **'***類型***'**  
 限制結果集包含只有在其上的資料庫指定的複寫選項*類型*已啟用值。 *型別*是**sysname**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**發行**|允許異動複寫。|  
|**合併式發行**|允許合併式複寫。|  
|**允許的複寫**（預設值）|允許交易式或合併式複寫。|  
  
 [  **@reserved=** ]*保留*  
 指定是否傳回現有發行集和訂閱的資訊。 *保留*是**元**，預設值為 0。 如果**1**，結果集會包含有關所指定的資料庫是否有任何現有的發行集或訂閱。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|資料庫的名稱。|  
|**id**|**int**|資料庫識別碼。|  
|**transpublish**|**bit**|如果資料庫已啟用快照集或交易式發行;值**1**表示啟用快照式或交易式發行。|  
|**mergepublish**|**bit**|如果資料庫已啟用合併式發行;值**1**表示合併發行啟用。|  
|**dbowner**|**bit**|如果使用者是屬於**db_owner**值固定資料庫角色; **1**指出使用者為此角色的成員。|  
|**dbreadonly**|**bit**|是如果要將資料庫標示為唯讀。值**1**表示資料庫是唯讀的。|  
|**haspublications**|**bit**|是指資料庫是否有任何現有的發行集。值**1**表示有現有的發行集。|  
|**haspullsubscriptions**|**bit**|是指資料庫是否有任何現有的提取訂閱。值**1**表示那里現有的提取訂閱。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpreplicationdboption**用於快照式、 交易式和合併式複寫。  
  
## <a name="permissions"></a>Permissions  
 成員**sysadmin**固定的伺服器角色可以執行**sp_helpreplicationdboption**任何資料庫。 成員**db_owner**固定的資料庫角色可以執行**sp_helpreplicationdboption**該資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [sp_replicationdboption &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
