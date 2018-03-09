---
title: "範例：擷取員工資訊 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EXPLICIT mode
ms.assetid: 63cd6569-2600-485b-92b4-1f6ba09db219
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c3c7b4150738ac5dbf878014004c3bda20092e33
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="example-retrieving-employee-information"></a>範例：擷取員工資訊
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
此範例會擷取每個員工的員工識別碼及員工名稱。 在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中，employeeID 可以從 Employee 資料表中的 BusinessEntityID 資料行取得。 員工名稱可以從 Person 資料表取得。 BusinessEntityID 資料行可用於聯結資料表。  
  
 假設想要 FOR XML EXPLICIT 轉換產生 XML，如下所示：  
  
```  
<Employee EmpID="1" >  
  <Name FName="Ken" LName="Sánchez" />  
</Employee>  
...  
```  
  
 因為階層中有兩個層級，所以您要撰寫兩個 `SELECT` 查詢並套用 UNION ALL。 上述為第一個查詢，其會擷取 <`Employee`> 元素及其屬性的值。 查詢會將 `1` 指派為 <`Employee`> 元素的 `Tag` 值，並將 NULL 指派為 `Parent`，因為這是最上層元素。  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID AS [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 上述為第二個查詢。 它會擷取 <`Name`> 元素的值。 它會將 `2` 指派為 <`Name`> 元素的 `Tag` 值，並將 `1` 指派為識別 <`Employee`> 做為父系的 `Parent` 標記值。  
  
```  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID;  
```  
  
 您可以利用 `UNION AL`L 合併這些查詢、套用 `FOR XML EXPLICIT`，然後指定所需的 `ORDER BY` 子句。 您必須先按 `BusinessEntityID` 排序資料列集，然後再按名稱排序，讓名稱中的 NULL 值最先出現。 執行以下未使用 FOR XML 子句的查詢，就可以看見產生了通用資料表。  
  
 以下為最後查詢：  
  
```  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID as [Employee!1!EmpID],  
       NULL       as [Name!2!FName],  
       NULL       as [Name!2!LName]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       FirstName,   
       LastName   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
ON  E.BusinessEntityID = P.BusinessEntityID  
ORDER BY [Employee!1!EmpID],[Name!2!FName]  
FOR XML EXPLICIT;  
```  
  
 以下是部份結果：  
  
 `<Employee EmpID="1">`  
  
 `<Name FName="Ken" LName="Sánchez" />`  
  
 `</Employee>`  
  
 `<Employee EmpID="2">`  
  
 `<Name FName="Terri" LName="Duffy" />`  
  
 `</Employee>`  
  
 `...`  
  
 第一個 `SELECT` 會指定產生之資料列集中的資料行名稱。 這些名稱會形成兩個資料行群組。 資料行名稱中有 `Tag` 值 `1` 的群組，可將 `Employee` 識別為元素，並將 `EmpID` 識別為屬性。 其他資料行群組在資料行中有 `Tag` 值 `2`，而且可將 <`Name`> 識別為元素，並將 `FName` 及 `LName` 識別為屬性。  
  
 下表會顯示此查詢產生的部分資料列集：  
  
 `Tag Parent  Employee!1!EmpID Name!2!FName Name!2!LName`  
  
 `--- ------  ---------------- ------------ ------------`  
  
 `1   NULL    1                NULL         NULL`  
  
 `2   1       1                Ken          Sánchez`  
  
 `1   NULL    2                NULL         NULL`  
  
 `2   1       2                Terri        Duffy`  
  
 `1   NULL    3                NULL         NULL`  
  
 `2   1       3                Roberto      Tamburello`  
  
 `...`  
  
 以下是如何處理通用資料表的資料列，以產生結果 XML 樹狀結構：  
  
 第一個資料列會識別 `Tag` 值 `1`。 因此，會識別 `Tag` 值 `1` 的資料行群組 `Employee!1!EmpID`。 此資料行會將 `Employee` 識別為元素名稱。 然後就會建立擁有 `EmpID` 屬性的 <`Employee`> 元素。 對應的資料行值會指派給這些屬性。  
  
 第二個資料列具有 `Tag` 值 `2`。 因此，會識別資料行名稱中 `Tag` 值為 `2` 的資料行群組 `Name!2!FName`、 `Name!2!LName`。 這些資料行名稱會將 `Name` 識別為元素名稱。 此外會建立擁有 `FName` 與 `LName` 屬性的 <`Name`> 元素。 然後將對應的資料行值指派給這些屬性。 此資料列會將 `1` 識別為 `Parent`。 此元素子系便會加入到先前的 <`Employee`> 元素。  
  
 這個處理序會對資料列集中其餘的資料列重複進行。 請記下通用資料表中資料列排序的優先順序，如此 FOR XML EXPLICIT 就可以依序處理資料列集，並產生您想要的 XML。  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 EXPLICIT 模式](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
