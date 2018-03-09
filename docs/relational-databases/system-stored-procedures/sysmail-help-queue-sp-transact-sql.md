---
title: "sysmail_help_queue_sp (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_help_queue_sp
- sysmail_help_queue_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_queue_sp
ms.assetid: 94840482-112c-4654-b480-9b456c4c2bca
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e83aba8601f4329a496229eca329035a95b283c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailhelpqueuesp-transact-sql"></a>sysmail_help_queue_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Database Mail 中有兩個佇列：郵件佇列和狀態佇列。 郵件佇列儲存等候傳送的郵件項目。 狀態佇列儲存已傳送之項目的狀態。 這個預存程序可檢視郵件或狀態佇列的狀態。 如果參數 **@queue_type** 未指定，預存程序傳回一個資料列的每個佇列。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_help_queue_sp  [ @queue_type = ] 'queue_type'  
```  
  
## <a name="arguments"></a>引數  
 [ **@queue_type** = ] **'***queue_type***'**  
 選擇性引數會刪除指定類型的電子郵件*類型*。 *類型*是**nvarchar(6)**沒有預設值。 有效的項目是**郵件**和**狀態**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**queue_type**|**nvarchar(6)**|佇列的類型。 可能的值為**郵件**和**狀態**。|  
|**長度**|**int**|指定佇列中的郵件項目數。|  
|**狀態**|**nvarchar(64)**|監視器的狀態。 可能的值為**INACTIVE** （佇列為非作用中）， **NOTIFIED** (佇列已受通知要進行接收)，和**RECEIVES_OCCURRING** （接收佇列）。|  
|**last_empty_rowset_time**|**日期時間**|佇列上次空的日期和時間。 以軍用時間格式和 GMT 時區表示。|  
|**last_activated_time**|**日期時間**|佇列上次啟動的日期和時間。 以軍用時間格式和 GMT 時區表示。|  
  
## <a name="remarks"></a>備註  
 當 Database Mail 進行疑難排解，使用**sysmail_help_queue_sp**若要查看佇列中有多少項目，啟用狀態的佇列，以及最後一次。  
  
## <a name="permissions"></a>Permissions  
 根據預設，只有**sysadmin**固定的伺服器角色可以存取這個程序。  
  
## <a name="examples"></a>範例  
 下列範例會傳回郵件和狀態佇列兩者。  
  
```  
EXECUTE msdb.dbo.sysmail_help_queue_sp ;  
GO  
```  
  
 這是已經編輯過長度的範例結果集。  
  
```  
queue_type length      state              last_empty_rowset_time  last_activated_time  
---------- -------- ------------------ ----------------------- -----------------------  
mail       0        RECEIVES_OCCURRING 2005-10-07 21:14:47.010 2005-10-10 20:52:51.517  
status     0        INACTIVE           2005-10-07 21:04:47.003 2005-10-10 21:04:47.003  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)  
  
  
