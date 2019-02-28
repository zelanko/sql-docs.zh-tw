---
title: PERCENTILE_DISC (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PERCENTILE_DISC
- PERCENTILE_DISC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PERCENTILE_DISC function
- analytic functions,PERCENTILE_DISC
ms.assetid: b545413d-c4f7-4c8e-8617-607599a26680
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1ae6754923dcb22a64251b351f013069b3a681fb
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56291816"
---
# <a name="percentiledisc-transact-sql"></a>PERCENTILE_DISC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中計算整個資料列集或資料列集特定資料分割的特定排序值百分位數。 針對指定的百分位數值 *P*，PERCENTILE_DISC 會在 ORDER BY 子句中排序運算式值。 接著傳回大於或等於*P* 所指定最小 CUME_DIST 值的值 (相對於相同的排序規格)。例如，PERCENTILE_DISC (0.5) 會計算運算式的第 50 個百分位數 (亦即中間值)。 PERCENTILE_DISC 會根據資料行值的離散分布計算百分位數。 結果等於某個特定的資料行值。  
  
 ![文章連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
PERCENTILE_DISC ( numeric_literal ) WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>引數  
 *literal*  
 要運算的百分位數。 值範圍必須介於 0.0 到 1.0 之間。  
  
 WITHIN GROUP **(** ORDER BY *order_by_expression* [ **ASC** | DESC)**  
 指定要用以排序及計算百分位數的值清單。 只允許一個 *order_by_expression*。 預設排序順序為遞增。 值的清單可以是任何能用於排序作業的有效資料類型。  
  
 OVER **(** \<partition_by_clause>)**  
 將 FROM 子句的結果集分成幾個資料分割。 百分位數函式會套用到這些資料分割。 如需詳細資訊，請參閱 [OVER 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)。 PERCENTILE_DISC 函式中不能指定 \<ORDER BY 子句> 和 \<資料列或範圍子句>。  
  
## <a name="return-types"></a>傳回類型  
 傳回型別由 *order_by_expression* 類型決定。  
  
## <a name="compatibility-support"></a>相容性支援  
 WITHIN GROUP 在相容性層級 110 及更高之下屬於保留的關鍵字。 如需詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
## <a name="general-remarks"></a>一般備註  
 資料集中所有的 Null 皆會予以忽略。  
  
 PERCENTILE_DISC 不具決定性。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="basic-syntax-example"></a>基本語法範例  

 下列範例會使用 PERCENTILE_CONT 和 PERCENTILE_DISC 尋找各部門員工的薪資中間值。 它們可能不會傳回相同的值：
* PERCENTILE_CONT 會傳回適當的值，即使它不存在於資料集中。
* PERCENTILE_DISC 會傳回實際的設定值。  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="basic-syntax-example"></a>基本語法範例  

 下列範例會使用 PERCENTILE_CONT 和 PERCENTILE_DISC 尋找各部門員工的薪資中間值。 它們可能不會傳回相同的值：
* PERCENTILE_CONT 會傳回適當的值，即使它不存在於資料集中。 
* PERCENTILE_DISC 會傳回實際的設定值。  
  
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
Shipping and Receiving  9.250000     9.0000
```  
  
## <a name="see-also"></a>另請參閱  
 [PERCENTILE_CONT &#40;Transact-SQL&#41;](../../t-sql/functions/percentile-cont-transact-sql.md)  
  
  


