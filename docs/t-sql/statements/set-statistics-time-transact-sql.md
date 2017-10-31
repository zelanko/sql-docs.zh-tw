---
title: "設定統計資料的時間 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_TIME_TSQL
- SET STATISTICS TIME
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], statement processing
- time [SQL Server], statement processing statistics
- SET STATISTICS TIME statement
- STATISTICS TIME option
- statements [SQL Server], statistical information
- parsing [SQL Server], SET STATISTICS TIME statement
- compile times [SQL Server]
- execution processing time [SQL Server]
ms.assetid: eec2e1cd-a29d-4cf3-a271-be9d61506f15
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: acd4684ea6b44f3a7371424eb6c90305e78841fc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-statistics-time-transact-sql"></a>SET STATISTICS TIME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  顯示剖析、編譯和執行每個陳述式所需要的毫秒數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SET STATISTICS TIME { ON | OFF }  
```  
  
## <a name="remarks"></a>備註  
 當 SET STATISTICS TIME 是 ON 時，會顯示陳述式的時間統計資料。 當它是 OFF 時，不會顯示時間統計資料。  
  
 SET STATISTICS TIME 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
 Microsoft[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]無法提供準確的統計資料在 fiber 模式下，當您啟用會啟動**輕量型共用**組態選項。  
  
 **Cpu**中的資料行**sysprocesses** SET STATISTICS TIME ON 來執行查詢時，才會更新資料表。 當 SET STATISTICS TIME 是 OFF， **0**傳回。  
  
 ON 和 OFF 設定也會影響 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中目前活動的 [處理序資訊] 檢視中的 CPU 資料行。  
  
## <a name="permissions"></a>Permissions  
 若要使用 SET STATISTICS TIME，使用者必須有執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的適當權限。 不需要 SHOWPLAN 權限。  
  
## <a name="examples"></a>範例  
 這個範例會顯示伺服器的執行、剖析和編譯階段。  
  
```  
USE AdventureWorks2012;  
GO         
SET STATISTICS TIME ON;  
GO  
SELECT ProductID, StartDate, EndDate, StandardCost   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS TIME OFF;  
GO  
```  
  
 以下為結果集：  
  
```  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
(269 row(s) affected)  
  
SQL Server Execution Times:  
   CPU time = 0 ms,  elapsed time = 2 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET STATISTICS IO & #40;TRANSACT-SQL & #41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  

