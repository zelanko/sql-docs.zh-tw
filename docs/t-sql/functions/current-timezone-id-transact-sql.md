---
title: CURRENT_TIMEZONE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CURRENT_TIMEZONE)ID
- CURRENT_TIMEZONE_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- current time zone id [SQL Server]
- current timezoneid [SQL Server]
- system time zone id[SQL Server]
- system timezone id[SQL Server]
- functions [SQL Server], time zone id
- functions [SQL Server], timezoneid
- timezoneid [SQL Server], functions
- time zone id [SQL Server], functions
- CURRENT_TIMEZONE_ID function [SQL Server]
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 3cadc9cd33fd1cdabb96cf450ad09253fdd435d1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85684625"
---
# <a name="current_timezone_id-transact-sql"></a>CURRENT_TIMEZONE_ID (Transact-SQL)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

此函式會傳回伺服器或執行個體所觀察到時區的識別碼。 針對 Azure SQL 受控執行個體，傳回的值是以執行個體本身在執行個體建立期間受指派時區為基礎，而不是以基礎作業系統的時區為基礎。
  
> [!NOTE]  
> 針對單一和集區 SQL Database，時區一律會設為 UTC，且 `CURRENT_TIMEZONE_ID` 會傳回 UTC 時區的識別碼。
  
## <a name="syntax"></a>語法  
  
```sql
CURRENT_TIMEZONE_ID ( )  
```
  
## <a name="arguments"></a>引數

這個函數沒有引數。
  
## <a name="return-type"></a>傳回類型  

**varchar**
  
## <a name="remarks"></a>備註  

`CURRENT_TIMEZONE_ID` 是非決定性函數。 參考這個資料行的檢視和運算式，是無法編製索引的。
  
## <a name="example"></a>範例

傳回值將會反映伺服器或執行個體的實際時區和語言設定。

```sql
SELECT CURRENT_TIMEZONE_ID();  
/* Returned:  
W. Europe Standard Time
*/
```  
  
## <a name="see-also"></a>另請參閱

[SQL Database 受控執行個體時區](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-timezone) \(機器翻譯\)

[CURRENT_TIMEZONE()](https://docs.microsoft.com/sql/t-sql/functions/current-timezone-transact-sql)
