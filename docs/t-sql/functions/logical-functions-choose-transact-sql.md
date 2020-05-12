---
title: CHOOSE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHOOSE
- CHOOSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHOOSE function
ms.assetid: 1c382c83-7500-4bae-bbdc-c1dbebd3d83f
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: d8a2f9871cbf547e465ef82049f23fcad9988d64
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82822885"
---
# <a name="logical-functions---choose-transact-sql"></a>邏輯函式 - CHOOSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中從數值清單傳回指定之索引的項目。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
  
CHOOSE ( index, val_1, val_2 [, val_n ] )  
```  
  
## <a name="arguments"></a>引數  
 *index*  
 表示以 1 為基底之索引到其後之項目清單中的整數運算式。  
  
 如果已提供的索引值具有數值資料類型，而非 **int**，則此數值會隱含地轉換成整數。 如果索引值超過數值陣列的界限，則 CHOOSE 會傳回 null。  
  
 *val_1 ... val_n*  
 任何資料類型的逗號分隔值清單。  
  
## <a name="return-types"></a>傳回型別  
 從通過功能的類型集中，傳回優先順序最高的資料類型。 如需詳細資訊，請參閱[資料類型優先順序 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="remarks"></a>備註  
 CHOOSE 作用類似陣列中的索引，其中的陣列是由跟隨索引引數的引數所組成。 其中 time-precision 引數會決定傳回值的秒數有效位數。  
  
## <a name="examples"></a>範例  

### <a name="a-simple-choose-example"></a>A. 簡易 CHOOSE 範例

 下列範例會從已提供的數值清單傳回第三個項目。  
 
```  
SELECT CHOOSE ( 3, 'Manager', 'Director', 'Developer', 'Tester' ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
-------------  
Developer  
  
(1 row(s) affected)  
```  

### <a name="b-simple-choose-example-based-on-column"></a>B. 以資料行為基礎的簡易 CHOOSE 範例

 下列範例會根據 `ProductCategoryID` 資料行中的值傳回簡單的字元字串。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductCategoryID, CHOOSE (ProductCategoryID, 'A','B','C','D','E') AS Expression1  
FROM Production.ProductCategory;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ProductCategoryID Expression1  
----------------- -----------  
3                 C  
1                 A  
2                 B  
4                 D  
  
(4 row(s) affected)  
  
```  

### <a name="c-choose-in-combination-with-month"></a>C. 搭配 MONTH 使用 CHOOSE
  
 下列範例會傳回雇用員工的季節。 MONTH 函數用於從 `HireDate` 資料行傳回月份的值。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT JobTitle, HireDate, CHOOSE(MONTH(HireDate),'Winter','Winter', 'Spring','Spring','Spring','Summer','Summer',   
                                                  'Summer','Autumn','Autumn','Autumn','Winter') AS Quarter_Hired  
FROM HumanResources.Employee  
WHERE  YEAR(HireDate) > 2005  
ORDER BY YEAR(HireDate);  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
JobTitle                                           HireDate   Quarter_Hired  
-------------------------------------------------- ---------- -------------  
Sales Representative                               2006-11-01 Autumn  
European Sales Manager                             2006-05-18 Spring  
Sales Representative                               2006-07-01 Summer  
Sales Representative                               2006-07-01 Summer  
Sales Representative                               2007-07-01 Summer  
Pacific Sales Manager                              2007-04-15 Spring  
Sales Representative                               2007-07-01 Summer  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [IIF &#40;Transact-SQL&#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)  
  
  
