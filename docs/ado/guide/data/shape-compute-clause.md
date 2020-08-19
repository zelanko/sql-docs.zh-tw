---
description: Shape COMPUTE 子句
title: Shape COMPUTE 子句 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
author: rothja
ms.author: jroth
ms.openlocfilehash: 9513666eca4d9e191b74b8a1a25dd8a9da051ee8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452840"
---
# <a name="shape-compute-clause"></a>Shape COMPUTE 子句
Shape COMPUTE 子句會產生父 **記錄集**，其資料行是由子 **記錄集**的參考所組成;選擇性資料行，其內容為章節、新的或匯出資料行，或在子 **記錄集** 或先前成形的 **記錄集**上執行彙總函式的結果;以及選擇性 BY 子句中所列之子 **記錄集** 的任何資料行。  
  
## <a name="syntax"></a>語法  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>描述  
 此子句的部分如下所示：  
  
 *child-command*  
 包含下列其中一項：  
  
-   以大括弧括住的查詢命令 ( " {} " ) 會傳回 **子記錄集** 物件。 此命令會發出至基礎資料提供者，而且其語法取決於該提供者的需求。 這通常是 SQL 語言，雖然 ADO 不需要任何特定的查詢語言。  
  
-   現有形狀 **記錄集**的名稱。  
  
-   另一個圖形命令。  
  
-   資料表關鍵字，後面接著資料提供者中的資料表名稱。  
  
 *child-alias*  
 用來參考*子命令*所傳回之**記錄集**的別名。 COMPUTE 子句的資料行清單中需要有 *子別名* ，而且會定義父和子 **記錄集** 物件之間的關聯性。  
  
 *appended-column-list*  
 此清單中的每個專案都會定義所產生父系中的資料行。 每個元素都包含一個章節資料行、一個新的資料行、一個計算結果欄，或子 **記錄集**上的彙總函式所產生的值。  
  
 *grp-field-list*  
 父記錄和子 **記錄集** 物件中的資料行清單，可指定如何在子系中群組資料列。  
  
 針對 *grp 欄位清單* 中的每個資料行，在子系和父 **記錄集** 物件中都有對應的資料行。 針對父 **記錄集**內的每個資料列， *grp 欄位清單* 資料行都有唯一的值，而且父資料列所參考的子 **記錄集** 只包含子資料列，其 *grp 欄位清單* 資料行的值與父資料列的值相同。  
  
 如果包含 BY 子句，則會根據 COMPUTE 子句中的資料行將子 **記錄集**的資料列分組。 父 **記錄集會** 針對子 **記錄集中**的每個資料列群組，各包含一個資料列。  
  
 如果省略 BY 子句，則整個子 **記錄集會** 被視為單一群組，且父 **記錄集** 只會包含一個資料列。 該資料列會參考整個子 **記錄集**。 省略 BY 子句可讓您計算整個子 **記錄集**的「總計」匯總。  
  
 例如：  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 無論父 **記錄集** 的格式為何 (使用計算或使用附加) ，它將包含用來將它與子 **記錄集**相關聯的章節資料行。 如果您想要的話，父 **記錄集** 也可以包含資料行，而這些資料行包含 (SUM、MIN、MAX 等的匯總，) 子資料列。 父 **記錄集和子記錄集** 都可能包含資料列，其中包含 **記錄集**內資料列上的運算式，以及新的和一開始是空的資料行。  
  
## <a name="operation"></a>作業  
 *子命令*會發出至提供者，以傳回子**記錄集**。  
  
 COMPUTE 子句會指定父 **記錄集**的資料行，這可能是子 **記錄集**的參考、一或多個匯總、匯出運算式或新的資料行。 如果有 BY 子句，則它定義的資料行也會附加至父 **記錄集**。 BY 子句會指定如何將子 **記錄集** 的資料列分組。  
  
 例如，假設您有一個名為「人口統計」的資料表，其中包含州、城市和人口欄位。  (資料表中的人口數位只提供作為範例) 。  
  
|State|城市|母體|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|或者|梅德福|200,000|  
|或者|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|San Diego|600,000|  
|WA|Tacoma|500,000|  
|或者|Corvallis|300,000|  
  
 現在，發出此圖形命令：  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 此命令會開啟具有兩個層級的成形 **記錄集** 。 父層級是產生的 **記錄集** ，其中包含匯總資料行 (`SUM(rs.population)`) 、參考子 **記錄集** () 的資料行 `rs` ，以及用來將子 **記錄集** 群組 () 的資料行 `state` 。 子層級是查詢命令 () 所傳回的 **記錄集** `select * from demographics` 。  
  
 子 **記錄集** 詳細資料列將依狀態分組，但不是特定的順序。 也就是說，這些群組不會以字母或數位順序排序。 如果您想要排序父 **記錄集** ，可以使用 **記錄集排序** 方法來排序父 **記錄集**。  
  
 您現在可以流覽開啟的父 **記錄集** ，並存取子詳細資料 **記錄集** 物件。 如需詳細資訊，請參閱 [存取階層式記錄集中](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)的資料列。  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>結果的父系和子詳細資料集  
  
### <a name="parent"></a>父系  
  
|SUM (rs。人口) |rs|State|  
|---------------------------|--------|-----------|  
|1,300,000|Child1 的參考|CA|  
|1,200,000|Child2 的參考|WA|  
|1,100,000|Child3 的參考|或者|  
  
## <a name="child1"></a>Child1  
  
|State|城市|母體|  
|-----------|----------|----------------|  
|CA|Los Angeles|800,000|  
|CA|San Diego|600,000|  
  
## <a name="child2"></a>Child2  
  
|State|城市|母體|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|WA|Tacoma|500,000|  
  
## <a name="child3"></a>Child3  
  
|State|城市|母體|  
|-----------|----------|----------------|  
|或者|梅德福|200,000|  
|或者|Portland|400,000|  
|或者|Corvallis|300,000|  
  
## <a name="see-also"></a>另請參閱  
 [存取階層式記錄集中的資料列](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [資料成形總覽](../../../ado/guide/data/data-shaping-overview.md)   
 [Field 物件](../../../ado/reference/ado-api/field-object.md)   
 [正式式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [ (ADO) 的記錄集物件 ](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [資料成形所需的提供者](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [一般圖形命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [ (ADO) 的 Value 屬性 ](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic for Applications 函式](../../../ado/guide/data/visual-basic-for-applications-functions.md)
