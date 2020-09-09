---
description: sysmail_help_queue_sp (Transact-SQL)
title: sysmail_help_queue_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_queue_sp
- sysmail_help_queue_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_queue_sp
ms.assetid: 94840482-112c-4654-b480-9b456c4c2bca
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 18e7e8d96a766f628f15dfc747fc3154bc95ea57
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547234"
---
# <a name="sysmail_help_queue_sp-transact-sql"></a>sysmail_help_queue_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Database Mail 中有兩個佇列：郵件佇列和狀態佇列。 郵件佇列儲存等候傳送的郵件項目。 狀態佇列儲存已傳送之項目的狀態。 這個預存程序可檢視郵件或狀態佇列的狀態。 如果未指定參數** \@ queue_type** ，預存程式會針對每個佇列傳回一個資料列。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_help_queue_sp  [ @queue_type = ] 'queue_type'  
```  
  
## <a name="arguments"></a>引數  
`[ @queue_type = ] 'queue_type'` 選擇性引數會刪除指定為 *queue_type*之類型的電子郵件。 *queue_type* 是 **Nvarchar (6) ** 沒有預設值。 有效的專案是 **mail** 和 **status**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**queue_type**|**Nvarchar (6) **|佇列的類型。 可能的值為 **mail** 和 **status**。|  
|**length**|**int**|指定佇列中的郵件項目數。|  
|**state**|**Nvarchar (64) **|監視器的狀態。 可能的值為 **非** 使用中 (佇列為非使用中) 、 **通知 (佇列** 已通知回條發生) **，以及 RECEIVES_OCCURRING (佇列** 接收) 。|  
|**last_empty_rowset_time**|**Datetime**|佇列上次空的日期和時間。 以軍用時間格式和 GMT 時區表示。|  
|**last_activated_time**|**Datetime**|佇列上次啟動的日期和時間。 以軍用時間格式和 GMT 時區表示。|  
  
## <a name="remarks"></a>備註  
 針對 Database Mail 進行疑難排解時，請使用 **sysmail_help_queue_sp** 來查看佇列中有多少專案、佇列的狀態，以及上次啟用的時間。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠存取此程式。  
  
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
  
  
