---
title: sp_replmonitorhelpmergesessiondetail (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpmergesessiondetail
- sp_replmonitorhelpmergesessiondetail_TSQL
helpviewer_keywords:
- sp_replmonitorhelpmergesessiondetail
ms.assetid: 805c92fc-3169-410c-984d-f37e063b791d
author: stevestein
ms.author: sstein
ms.openlocfilehash: b1aaa8afdb6ad67f906140c0714f115b64c08bc1
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68764434"
---
# <a name="spreplmonitorhelpmergesessiondetail-transact-sql"></a>sp_replmonitorhelpmergesessiondetail (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  傳回有關用來監視合併式複寫之特定複寫合併代理程式工作階段的詳細發行項層級資訊。 結果集包含在工作階段期間同步處理的每個發行項各一個詳細資料列。 同時也包含代表工作階段初始化的一個資料列，以及摘要工作階段之上傳和下載階段的資料列。 這個預存程序執行於散發資料庫的散發者端，或訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replmonitorhelpmergesessiondetail [ @session_id = ] session_id  
```  
  
## <a name="arguments"></a>引數  
`[ @session_id = ] session_id`指定代理程式會話。 *session_id*是**int** , 沒有預設值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**PhaseID**|**int**|這是同步處理工作階段的階段，它可以是下列其中一項：<br /><br /> **0** = 初始化或摘要資料列<br /><br /> **1** = 上傳<br /><br /> **2** = 下載|  
|**ArticleName**|**sysname**|這是正在同步處理的發行項名稱。 **ArticleName**也包含結果集中不代表發行項詳細資料之資料列的摘要資訊。|  
|**PercentComplete**|**decimal**|針對目前執行中或已失敗的工作階段，指出套用在給定發行項詳細資料列的總變更量之百分比。|  
|**RelativeCost**|**decimal**|指出同步處理發行項所花的時間，相當於該工作階段同步處理總時間的百分比。|  
|**有效期間**|**int**|代理程式工作階段的長度。|  
|**Inserts**|**int**|工作階段中的插入數。|  
|**Updates**|**int**|工作階段中的更新數。|  
|**Deletes**|**int**|工作階段中的刪除數。|  
|**衝突**|**int**|工作階段所發生的衝突數。|  
|**ErrorID**|**int**|工作階段錯誤的識別碼。|  
|**SeqNo**|**int**|結果集中的工作階段順序。|  
|**RowType**|**int**|指出結果集中每個資料列所代表的資訊類型。<br /><br /> **0** = 初始化<br /><br /> **1** = 上傳摘要<br /><br /> **2** = 發行項上傳詳細資料<br /><br /> **3** = 下載摘要<br /><br /> **4** = 發行項下載詳細資料|  
|**SchemaChanges**|**int**|工作階段中的結構描述變更數。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或**1** (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_replmonitorhelpmergesessiondetail**是用來監視合併式複寫。  
  
 在訂閱者上執行時, **sp_replmonitorhelpmergesessiondetail**只會傳回最後5個合併代理程式會話的詳細資訊。  
  
## <a name="permissions"></a>Permissions  
 只有「散發者」端或「訂閱者」端之訂閱資料庫上的**db_owner**或**replmonitor**固定資料庫角色的成員, 才能夠執行**sp_replmonitorhelpmergesessiondetail**。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
