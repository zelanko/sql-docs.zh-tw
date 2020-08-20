---
description: sys.sp_flush_log (Transact-SQL)
title: sys. sp_flush_log (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 99d804cc8df3a25853abc11b2ea4403b00fec503
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489026"
---
# <a name="syssp_flush_log-transact-sql"></a>sys.sp_flush_log (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  將目前資料庫的交易記錄排清至磁碟，因而強行寫入所有先前認可的延遲持久交易。  
  
 如果您是因為效能優勢而選擇要使用延遲的交易持久性，但又想要確保伺服器當機或容錯移轉時遺失的資料量有所限制，請定期執行 `sys.sp_flush_log`。 例如，如果您想要確保您不會遺失超過 x 秒的資料，就會 `sp_flush_log` 每隔 x 秒執行一次。  
  
 執行 `sys.sp_flush_log` 可保證所有先前認可的延遲持久交易都會變成持久。 如需詳細資訊，請參閱概念主題 [控制交易持久性](../../relational-databases/logs/control-transaction-durability.md) 。  
  
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
  
  
