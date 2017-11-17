---
title: "PERCENTILE_CONT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/20/2015
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
- PERCENTILE_CONT_TSQL
- PERCENTILE_CONT
dev_langs:
- TSQL
helpviewer_keywords:
- analytic functions, PERCENTILE_CONT
- PERCENTILE_CONT function
ms.assetid: d019419e-5297-4994-97d5-e9c8fc61bbf4
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 424e3ac668bb979a2d30446ff1ecb57346a0e8ac
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="percentilecont-transact-sql"></a>PERCENTILE_CONT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  依據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料行值連續分佈計算百分位數。 其結果會以內插值取代，可能不會等於資料行中的任何特定值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
PERCENTILE_CONT ( numeric_literal )   
    WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>引數  
 *numeric_literal*  
 要運算的百分位數。 值範圍必須介於 0.0 到 1.0 之間。  
  
 群組內**(** ORDER BY *order_by_expression* [ **ASC** |DESC]**)**  
 指定要用以排序及計算百分位數的數值清單。 只有一個*order_by_expression*允許。 運算式必須評估為精確數值類型 (**int**， **bigint**， **smallint**， **tinyint**，**數值**，**元**，**十進位**， **smallmoney**， **money**) 或近似數值類型 (**float**，**真實**)。 不允許其他資料類型。 預設排序順序為遞增。  
  
 透過**(** \<partition_by_clause > **)**  
 將 FROM 子句所產生的結果集，分割成套用百分位數函數的分割區。 如需詳細資訊，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md). \<ORDER BY 子句 > 及\<資料列或範圍子句 > 不可在 PERCENTILE_CONT 函數中指定 OVER 的語法。  
  
## <a name="return-types"></a>傳回類型  
 **float(53)**  
  
## <a name="compatibility-support"></a>相容性支援  
 WITHIN GROUP 在相容性層級 110 及更高之下屬於保留的關鍵字。 如需詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
## <a name="general-remarks"></a>一般備註  
 資料集中所有的 Null 皆會予以忽略。  
  
 PERCENTILE_CONT 不具決定性。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-basic-syntax-example"></a>A. 基本語法範例  
 下列範例會使用 PERCENTILE_CONT 及 PERCENTILE_DISC 尋找各部門員工的薪資中間值。 請注意，這些函數可能不會傳回相同的值。 這是因為資料集中無論有無 PERCENTILE_CONT，PERCENTILE_CONT 皆會插入適當值，而 PERCENTILE_DISC 則一律會傳回資料集中的實際值。  
  
```  
USE AdventureWorks2012;  
  
SELECT DISTINCT Name AS DepartmentName  
      ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianCont  
      ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianDisc  
FROM HumanResources.Department AS d  
INNER JOIN HumanResources.EmployeeDepartmentHistory AS dh   
    ON dh.DepartmentID = d.DepartmentID  
INNER JOIN HumanResources.EmployeePayHistory AS ph  
    ON ph.BusinessEntityID = dh.BusinessEntityID  
WHERE dh.EndDate IS NULL;  
```  
  
 以下為部分結果集。  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.8269      16.8269
Engineering            34.375       32.6923
Executive              54.32695     48.5577
Human Resources        17.427850    16.5865
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-basic-syntax-example"></a>B. 基本語法範例  
 下列範例會使用 PERCENTILE_CONT 及 PERCENTILE_DISC 尋找各部門員工的薪資中間值。 請注意，這些函數可能不會傳回相同的值。 這是因為資料集中無論有無 PERCENTILE_CONT，PERCENTILE_CONT 皆會插入適當值，而 PERCENTILE_DISC 則一律會傳回資料集中的實際值。  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT DepartmentName  
,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY BaseRate)  
    OVER (PARTITION BY DepartmentName) AS MedianCont  
,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY BaseRate)  
    OVER (PARTITION BY DepartmentName) AS MedianDisc  
FROM dbo.DimEmployee;  
  
```  
  
 以下為部分結果集。  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.826900    16.8269
Engineering            34.375000    32.6923
Human Resources        17.427850    16.5865
Shipping and Receiving 9.250000      9.0000
```  
  
## <a name="see-also"></a>另請參閱  
 [PERCENTILE_DISC &#40;TRANSACT-SQL &#41;](../../t-sql/functions/percentile-disc-transact-sql.md)  
  
  



