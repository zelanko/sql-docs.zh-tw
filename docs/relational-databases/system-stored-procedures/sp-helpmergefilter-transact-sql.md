---
title: sp_helpmergefilter （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergefilter
- sp_helpmergefilter_TSQL
helpviewer_keywords:
- sp_helpmergefilter
ms.assetid: f133a094-0009-4771-b93b-e86a5c01e40b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 487ae30ae57ac2111d23c26fd85a4ab049301b3d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775755"
---
# <a name="sp_helpmergefilter-transact-sql"></a>sp_helpmergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  傳回合併篩選的相關資訊。 這個預存程序執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpmergefilter [ @publication= ] 'publication'   
    [ , [ @article= ] 'article']  
    [ , [ @filtername= ] 'filtername']  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @article = ] 'article'`這是發行項的名稱。 發行項是**sysname**，預設*值是*，它會傳回 **%** 所有發行項的名稱。  
  
`[ @filtername = ] 'filtername'`這是要傳回信息的篩選器名稱。 *filtername*是**sysname**，預設值是 **%** ，它會傳回發行項或發行集所定義之所有篩選的相關資訊。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**join_filterid**|**int**|聯結篩選的識別碼。|  
|**filtername**|**sysname**|篩選的名稱。|  
|**join article name**|**sysname**|聯結發行項的名稱。|  
|**join_filterclause**|**Nvarchar （2000）**|限定聯結的篩選子句。|  
|**join_unique_key**|**int**|聯結是否基於唯一索引鍵。|  
|**base table owner**|**sysname**|基底資料表的擁有者名稱。|  
|**base table name**|**sysname**|基底資料表的名稱。|  
|**join table owner**|**sysname**|聯結到基底資料表中之資料表的擁有者名稱。|  
|**join table name**|**sysname**|聯結到基底資料表中的資料表名稱。|  
|**article name**|**sysname**|聯結到基底資料表中的資料表發行項名稱。|  
|**filter_type**|**tinyint**|合併篩選的類型，它可以是下列項目之一：<br /><br /> **1** = 僅聯結篩選<br /><br /> **2** = 邏輯記錄關聯性<br /><br /> **3** = 兩者|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpmergefilter**用於合併式複寫中。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色和**db_owner**固定資料庫角色的成員，才能夠執行**sp_helpmergefilter**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addmergefilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
