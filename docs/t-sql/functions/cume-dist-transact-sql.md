---
title: "CUME_DIST (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CUME_DIST
- CUME_DIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CUME_DIST function
- analytic functions, CUME_DIST
ms.assetid: 491b07f3-9ffd-4cdd-93e5-5abb636fc5ef
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 22364fce2c5c8bfa2707f1f270dd728735096a31
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="cumedist-transact-sql"></a>CUME_DIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

計算 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中之值群組內某值的累加分配。 亦即，CUME_DIST 會計算值群組中某值的相對位置。 資料列*r*，此時是假設遞增排序的 CUME_DIST *r*是值的資料列數目，小於或等於值*r*，除以資料列數目評估資料分割或查詢結果集內。 CUME_DIST 與 PERCENT_RANK 函數類似。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CUME_DIST( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
  
```  
  
## <a name="arguments"></a>引數  
透過**(** [ *partition_by_clause* ] *order_by_clause***)**  
*partition_by_clause*將分割成資料分割要套用函式的 FROM 子句所產生的結果集。 如未指定，此函數會將查詢結果集的所有資料列視為單一群組。 *order_by_clause*決定執行作業的邏輯順序。 *order_by_clause*需要。 \<資料列或範圍子句 > 無法在 CUME_DIST 函數中指定 OVER 的語法。 如需詳細資訊，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>傳回型別
**float(53)**
  
## <a name="remarks"></a>備註  
CUME_DIST 傳回的值範圍大於 0 並小於或等於 1。 繫結值的計算所得一律會是相同的累計分佈值。 預設會包含 NULL 值，並將其視為最低值。
  
CUME_DIST 不具決定性。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。
  
## <a name="examples"></a>範例  
下列範例使用 CUME_DIST 函數計算給定部門中之各員工的薪資百分位數。 CUME_DIST 函數傳回的值代表薪資小於或等於相同部門中現行員工的員工數百分比。 PERCENT_RANK 函數會以百分比計算該員工薪資在部門內的次序。 指定 PARTITION BY 子句的目的，在依部門分割結果集中的資料列。 OVER 子句中的 ORDER BY 子句會將每個分割區中的資料列以邏輯方式排序。 SELECT 陳述式中的 ORDER BY 子句會決定結果集的顯示排序。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT Department, LastName, Rate,   
       CUME_DIST () OVER (PARTITION BY Department ORDER BY Rate) AS CumeDist,   
       PERCENT_RANK() OVER (PARTITION BY Department ORDER BY Rate ) AS PctRank  
FROM HumanResources.vEmployeeDepartmentHistory AS edh  
    INNER JOIN HumanResources.EmployeePayHistory AS e    
    ON e.BusinessEntityID = edh.BusinessEntityID  
WHERE Department IN (N'Information Services',N'Document Control')   
ORDER BY Department, Rate DESC;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
  
Department             LastName               Rate                  CumeDist               PctRank  
---------------------- ---------------------- --------------------- ---------------------- ----------------------  
Document Control       Arifin                 17.7885               1                      1  
Document Control       Norred                 16.8269               0.8                    0.5  
Document Control       Kharatishvili          16.8269               0.8                    0.5  
Document Control       Chai                   10.25                 0.4                    0  
Document Control       Berge                  10.25                 0.4                    0  
Information Services   Trenary                50.4808               1                      1  
Information Services   Conroy                 39.6635               0.9                    0.888888888888889  
Information Services   Ajenstat               38.4615               0.8                    0.666666666666667  
Information Services   Wilson                 38.4615               0.8                    0.666666666666667  
Information Services   Sharma                 32.4519               0.6                    0.444444444444444  
Information Services   Connelly               32.4519               0.6                    0.444444444444444  
Information Services   Berg                   27.4038               0.4                    0  
Information Services   Meyyappan              27.4038               0.4                    0  
Information Services   Bacon                  27.4038               0.4                    0  
Information Services   Bueno                  27.4038               0.4                    0  
(15 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
[PERCENT_RANK &#40;TRANSACT-SQL &#41;](../../t-sql/functions/percent-rank-transact-sql.md)
  
  

