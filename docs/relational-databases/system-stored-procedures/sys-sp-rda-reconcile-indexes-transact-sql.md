---
title: sys. sp_rda_reconcile_indexes (Transact-sql) |Microsoft Docs
description: 瞭解 sys. sp_rda_reconcile_indexes。 瞭解如何使用這個 Transact-sql 預存程式將架構工作排入佇列，以協調遠端資料表上的索引。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reconcile_indexes
- sp_rda_reconcile_indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_indexes stored procedure
ms.assetid: 96b31ab9-bf84-46d6-9990-81f5c51f885a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2d224f5ea2b20f684fdd9e484304639114fd2d2e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544667"
---
# <a name="syssp_rda_reconcile_indexes-transact-sql"></a>sys. sp_rda_reconcile_indexes (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  將架構工作排入佇列，以協調遠端資料表上的索引。 順利完成此工作之後，遠端資料表會有相同的索引存在於已啟用本機 Stretch 的資料表上。  
  
 當您呼叫 **sp_rda_reconcile_indexes**時，如果有另一個工作排入佇列以協調索引，這個預存程式不會將重複的工作排入佇列。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_rda_reconcile_indexes [@objname = ] 'objname'  
  
```  
  
## <a name="arguments"></a>引數  
 [ @objname =] *' objname '*  
 這是您要對其進行協調之已啟用延展功能之資料表的限定名稱或非限定名稱。 只有當您指定限定物件時，才需要引號。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 >0 (失敗)   
  
## <a name="see-also"></a>另請參閱  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
