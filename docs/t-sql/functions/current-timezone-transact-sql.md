---
title: CURRENT_TIMEZONE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CURRENT_TIMEZONE
- CURRENT_TIMEZONE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- current time zone [SQL Server]
- current timezone [SQL Server]
- system time zone [SQL Server]
- system timezone [SQL Server]
- functions [SQL Server], time zone
- functions [SQL Server], timezone
- timezone [SQL Server], functions
- time zone [SQL Server], functions
- CURRENT_TIMEZONE function [SQL Server]
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: dcdae3ff107ad1e1e3a7bc58fde4248bb5330223
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62850378"
---
# <a name="currenttimezone-transact-sql"></a>CURRENT_TIMEZONE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ssver15-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

此函式傳回伺服器或執行個體所觀察到之時區的名稱。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`CURRENT_TIMEZONE` 會從執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之電腦的作業系統衍生這個傳回值。 SQL Database 受控執行個體傳回的值是根據執行個體本身在執行個體建立期間受指派的時區，而不是基礎作業系統的時區。
  
> [!NOTE]  
> 對於單一和集區 SQL Database，時區一律是設定為 UTC 且 `CURRENT_TIMEZONE` 會傳回 UTC 時區的名稱。
  
## <a name="syntax"></a>語法  
  
```sql
CURRENT_TIMEZONE ( )  
```
  
## <a name="arguments"></a>引數

這個函數沒有引數。
  
## <a name="return-type"></a>傳回類型  

**varchar**
  
## <a name="remarks"></a>Remarks  

`CURRENT_TIMEZONE` 是非決定性函數。 參考這個資料行的檢視和運算式，是無法編製索引的。
  
## <a name="example"></a>範例

請注意，傳回值將會反映伺服器或執行個體的實際時區和語言設定。

```sql
SELECT CURRENT_TIMEZONE();  
/* Returned:  
(UTC+01:00) Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna 
*/
```  
  
## <a name="see-also"></a>另請參閱

[SQL Database 受控執行個體時區](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-timezone) \(機器翻譯\)
