---
title: sys.sp_flush_log & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_flush_log_TSQL
- sys.sp_flush_log
- sys.sp_flush_log_TSQL
- sp_flush_log
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_flush_log
ms.assetid: 75cc9f52-3b1f-4754-b1e7-ce0dd3323bc9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 61c4cceab6c816d63226216a54d4f647e92e592d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066680"
---
# <a name="sysspflushlog-transact-sql"></a>sys.sp_flush_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  將目前資料庫的交易記錄排清至磁碟，因而強行寫入所有先前認可的延遲持久交易。  
  
 如果您是因為效能優勢而選擇要使用延遲的交易持久性，但又想要確保伺服器當機或容錯移轉時遺失的資料量有所限制，請定期執行 `sys.sp_flush_log`。 例如，如果您想要確定您不會遺失超過 x 秒價值的資料，您會執行`sp_flush_log`每隔 x 秒。  
  
 執行 `sys.sp_flush_log` 可保證所有先前認可的延遲持久交易都會變成持久。 請參閱概念性主題[控制交易持久性](../../relational-databases/logs/control-transaction-durability.md)如需詳細資訊。  
  
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
  
  
