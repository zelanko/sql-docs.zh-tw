---
title: "sys.sp_flush_log (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_flush_log_TSQL
- sys.sp_flush_log
- sys.sp_flush_log_TSQL
- sp_flush_log
dev_langs: TSQL
helpviewer_keywords: sys.sp_flush_log
ms.assetid: 75cc9f52-3b1f-4754-b1e7-ce0dd3323bc9
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d45bf1a883b61ccc975c0d3dd4d83086d88c7177
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="sysspflushlog-transact-sql"></a>sys.sp_flush_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  將目前資料庫的交易記錄排清至磁碟，因而強行寫入所有先前認可的延遲持久交易。  
  
 如果您是因為效能優勢而選擇要使用延遲的交易持久性，但又想要確保伺服器當機或容錯移轉時遺失的資料量有所限制，請定期執行 `sys.sp_flush_log`。 例如，假設您想要確保遺失的資料量不超過 x 秒，就應該每隔 x 秒執行 `sp_flush_log`。  
  
 執行 `sys.sp_flush_log` 可保證所有先前認可的延遲持久交易都會變成持久。 請參閱觀念性主題[控制交易持久性](../../relational-databases/logs/control-transaction-durability.md)如需詳細資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
  
sys.sp_flush_log  
  
```  
  
#### <a name="parameters"></a>參數  
 無。  
  
## <a name="return-code-values"></a>傳回碼值  
 傳回碼為 1 表示成功。  其他任何值都表示失敗。  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="sample-code"></a>範例程式碼  
  
```sql  
.  
EXECUTE sys.sp_flush_log  
  
```  
  
  
