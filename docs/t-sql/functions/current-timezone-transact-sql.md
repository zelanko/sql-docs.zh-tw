---
title: CURRENT_TIMEZONE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/28/2020
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
ms.openlocfilehash: 760da1491a7fbf4633cb02fe1fea8568e7ab9fa1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85684489"
---
# <a name="current_timezone-transact-sql"></a>CURRENT_TIMEZONE (Transact-SQL)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

此函式傳回伺服器或執行個體所觀察到之時區的名稱。 針對 SQL Database 受控執行個體，傳回的值是以執行個體本身在執行個體建立期間受指派的時區為基礎，而不是以底層作業系統的時區為基礎。
  
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
  
## <a name="remarks"></a>備註  

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

[CURRENT_TIMEZONE_ID()](https://docs.microsoft.com/sql/t-sql/functions/current-timezone-id-transact-sql)
