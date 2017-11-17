---
title: "SWITCHOFFSET (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/02/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SWITCHTZ
- SWITCHTZ_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- functions [SQL Server], time
- functions [SQL Server], date and time
- SWITCHOFFSET function [SQL Server]
- time [SQL Server], functions
- date and time [SQL Server], SWITCHOFFSET
- time zones [SQL Server]
ms.assetid: 32a48e36-0aa4-4260-9fe9-cae9197d16c5
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 3c81153c233e68d12347dc47ae9c232f4a5ee030
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="switchoffset-transact-sql"></a>SWITCHOFFSET (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回**datetimeoffset**從儲存的時區位移變更為指定的新時區位移的值。  
  
 如需所有[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和時間資料型別和函式，請參閱[日期和時間資料型別和函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SWITCHOFFSET ( DATETIMEOFFSET, time_zone )   
```  
  
## <a name="arguments"></a>引數  
 *DATETIMEOFFSET*  
 運算式是可解析成**datetimeoffset （n)**值。  
  
 *time_zone*  
 這是採用 [+|-]TZH:TZM 格式的字元字串或代表時區位移之帶正負號的整數 (秒鐘)，而且假設是日光節約感知且經過調整。  
  
## <a name="return-type"></a>傳回類型  
 **datetimeoffset**的小數有效位數與*DATETIMEOFFSET*引數。  
  
## <a name="remarks"></a>備註  
 使用 SWITCHOFFSET 來選取**datetimeoffset**一開始儲存的時區位移不同的時區位移值。 SWITCHOFFSET 不會更新儲存*time_zone*值。  
  
 SWITCHOFFSET 可用來更新**datetimeoffset**資料行。  
  
 使用 SWITCHOFFSET 搭配函數 GETDATE() 會導致查詢執行速度變慢。 這是因為查詢最佳化工具無法取得日期時間值的準確基數估計值。 若要解決此問題，請使用 OPTION (RECOMPILE) 查詢提示，強制查詢最佳化工具在下次執行相同的查詢時，重新編譯查詢計劃。 之後，最佳化工具會有準確的基數估計值，並將產生更有效率的查詢計劃。 如需 RECOMPILE 查詢提示的詳細資訊，請參閱[查詢提示 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
```  
DECLARE @dt datetimeoffset = switchoffset (CONVERT(datetimeoffset, GETDATE()), '-04:00');   
SELECT * FROM t    
WHERE c1 > @dt OPTION (RECOMPILE);  
  
```  
  
## <a name="examples"></a>範例  
 下列範例會使用 `SWITCHOFFSET` 來顯示與資料庫中儲存的值不同的時區位移。  
  
```  
CREATE TABLE dbo.test   
    (  
    ColDatetimeoffset datetimeoffset  
    );  
GO  
INSERT INTO dbo.test   
VALUES ('1998-09-20 7:45:50.71345 -5:00');  
GO  
SELECT SWITCHOFFSET (ColDatetimeoffset, '-08:00')   
FROM dbo.test;  
GO  
--Returns: 1998-09-20 04:45:50.7134500 -08:00  
SELECT ColDatetimeoffset  
FROM dbo.test;  
--Returns: 1998-09-20 07:45:50.7134500 -05:00  
```  
  
## <a name="see-also"></a>另請參閱  
 [CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [TIME ZONE &AMP;#40;TRANSACT-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  



