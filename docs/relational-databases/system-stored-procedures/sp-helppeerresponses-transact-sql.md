---
description: sp_helppeerresponses (Transact-SQL)
title: sp_helppeerresponses (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerresponses_TSQL
- sp_helppeerresponses
helpviewer_keywords:
- sp_helppeerresponses
ms.assetid: e55789d1-43fb-4a37-9e5e-60ccef122a5d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1b3918d773984223c450e11ead71d045bf21db6d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535122"
---
# <a name="sp_helppeerresponses-transact-sql"></a>sp_helppeerresponses (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回從點對點複寫拓撲中的參與者收到之特定狀態要求的所有回應，此要求是藉由在拓撲中任何發行的資料庫上執行 [sp_helppeerrequests](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) 來起始。 這個預存程序是在參與點對點複寫拓撲之發行者的發行集資料庫執行。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helppeerresponses [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>引數  
`[ @request_id = ] request_id` 這是特定狀態要求的識別碼。 *request_id* 是 **int**，沒有預設值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|狀態要求的識別碼。|  
|**同行**|**sysname**|產生回應的對等名稱。|  
|**peer_db**|**sysname**|在產生回應之對等的資料庫名稱。|  
|**received_date**|**datetime**|從傳送回應的對等處，要求器收到回應的日期和時間。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_helppeerresponses** 用於點對點異動複寫中。  
  
 還原點對點拓撲中發行的資料庫時，會使用**sp_helppeerresponses**程式。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_helppeerresponses**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_deletepeerrequesthistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
