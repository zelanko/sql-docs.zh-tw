---
title: p (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
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
- sp_gettopologyinfo_TSQL
- sp_gettopologyinfo
helpviewer_keywords:
- sp_gettopologyinfo
ms.assetid: 8bbe8a06-a4aa-4219-8402-12db6a4682c6
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d2a9e5031460c478806aacc9e7d97de593ee613
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spgettopologyinfo-transact-sql"></a>sp_gettopologyinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關點對點異動複寫拓撲的資訊。 執行[sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md)收集資訊，然後再執行此程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_gettopologyinfo [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>引數  
 [ @request_id=] *request_id*  
 這是拓撲狀態要求的識別碼。 *request_id*是**int**，預設值是 NULL。 若要取得識別碼，請使用@request_id輸出參數[sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md)或查詢[MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md)系統資料表。  
  
## <a name="result-sets"></a>結果集  
 sp_gettopologyinfo 會傳回具有單一 XML 資料行的結果集。 XML 資料行中的資料是中的資料相同[MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md)系統資料表。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 sp_gettopologyinfo 會用於點對點異動複寫中。 執行[sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md)您執行 sp_gettopologyinfo 之前。 這些程序是由「設定點對點拓撲精靈」所使用，但是如果您需要 XML 格式的拓撲資訊，也可以直接使用這些程序。 如果您偏愛表格式結果，請查詢[MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md)系統資料表。  
  
## <a name="permissions"></a>Permissions  
 需要系統管理員 (sysadmin) 固定伺服器角色或 db_owner 固定資料庫角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [點對點異動複寫](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
