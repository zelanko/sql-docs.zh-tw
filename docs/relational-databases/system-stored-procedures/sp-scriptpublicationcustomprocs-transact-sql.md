---
title: sp_scriptpublicationcustomprocs (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptpublicationcustomprocs
- sp_scriptpublicationcustomprocs_TSQL
helpviewer_keywords:
- sp_scriptpublicationcustomprocs
ms.assetid: b06102d5-4284-4834-b126-bc0baea49be5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2b57ae49875c07607e153b793c76db31d5dd347b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52808640"
---
# <a name="spscriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對啟用了自動產生自訂程序結構描述選項的發行集之所有資料表發行項，編寫自訂 INSERT、UPDATE 和 DELETE 程序的指令碼。 **sp_scriptpublicationcustomprocs**特別適合用來設定，可以手動套用快照集的訂閱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication**=] **'***publication_name***'**  
 這是發行集的名稱。 *publication_name*已**sysname**沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 傳回結果集，其中包含單一**nvarchar(4000)** 資料行。 這個結果集形成建立自訂預存程序時，所需要的完整 CREATE PROCEDURE 陳述式。  
  
## <a name="remarks"></a>備註  
 不含自動產生自訂程序 (0x2) 結構描述選項的發行項，並不編寫自訂程序的指令碼。  
  
 下列程序由**sp_scriptpublicationcustomprocs**建立程序，「 訂閱者 」，而且不應該直接執行：  
  
 **sp_script_reconciliation_delproc**  
  
 **sp_script_reconciliation_insproc**  
  
 **sp_script_reconciliation_vdelproc**  
  
 **sp_script_reconciliation_xdelproc**  
  
 **sp_scriptdelproc**  
  
 **sp_scriptinsproc**  
  
 **sp_scriptmappedupdproc**  
  
 **sp_scriptupdproc**  
  
 **sp_scriptvdelproc**  
  
 **sp_scriptvupdproc**  
  
 **sp_scriptxdelproc**  
  
 **sp_scriptxupdproc**  
  
## <a name="permissions"></a>Permissions  
 執行權限授與**公開金鑰**; 程序的安全性檢查執行這個預存程序來限制存取權的成員**sysadmin**固定的伺服器角色和**db_擁有者**目前資料庫中的固定的資料庫角色。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
