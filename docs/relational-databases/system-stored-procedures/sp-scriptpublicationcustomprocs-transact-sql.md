---
title: sp_scriptpublicationcustomprocs （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bb59b3ce367a7f936d4d8bec28b363e493857632
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82816562"
---
# <a name="sp_scriptpublicationcustomprocs-transact-sql"></a>sp_scriptpublicationcustomprocs (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  針對啟用了自動產生自訂程序結構描述選項的發行集之所有資料表發行項，編寫自訂 INSERT、UPDATE 和 DELETE 程序的指令碼。 **sp_scriptpublicationcustomprocs**特別適用于設定手動套用快照集的訂閱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication_name'`這是發行集的名稱。 *publication_name*是**sysname** ，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 傳回由單一**Nvarchar （4000）** 資料行所組成的結果集。 這個結果集形成建立自訂預存程序時，所需要的完整 CREATE PROCEDURE 陳述式。  
  
## <a name="remarks"></a>備註  
 不含自動產生自訂程序 (0x2) 結構描述選項的發行項，並不編寫自訂程序的指令碼。  
  
 **Sp_scriptpublicationcustomprocs**會使用下列程式來建立「訂閱者」的程式，而不應直接執行：  
  
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
  
## <a name="permissions"></a>權限  
 執行許可權會授與**public**;系統會在此預存程式內執行程式安全性檢查，以限制在目前資料庫中，對**sysadmin**固定伺服器角色的成員和**db_owner**固定資料庫角色的存取權。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
