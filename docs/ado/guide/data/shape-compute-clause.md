---
title: 圖形 COMPUTE 子句 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e1e268da5eb4c53b6270e474987c69b88383cd9b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700361"
---
# <a name="shape-compute-clause"></a>Shape COMPUTE 子句
Shape COMPUTE 子句會產生父代**資料錄集**，其資料行所組成的參考子系**資料錄集**; 選擇性資料行的內容是一章，新的或導出資料行，或對子系執行彙總函式的結果**Recordset**或先前的圖形化**資料錄集**; 以及從子系的任何資料行**資料錄集**中所列選擇性的 BY 子句。  
  
## <a name="syntax"></a>語法  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>描述  
 這個子句的部分如下所示：  
  
 *child-command*  
 包含下列其中一項：  
  
-   查詢命令，在大括號 ("{}")，傳回的子系**資料錄集**物件。 基礎資料提供者發出的命令和其語法取決於該提供者的需求。 這通常是 SQL 語言，雖然 ADO 不需要任何特定的查詢語言。  
  
-   現有的形狀名稱**資料錄集**。  
  
-   另一個圖形的命令。  
  
-   資料表關鍵字，後面加上資料表中的資料提供者的名稱。  
  
 *child-alias*  
 用來參考的別名**Recordset**所傳回*子命令。* *子系別名*必要的計算子句中的資料行清單中，且定義父系和子系之間的關聯性**資料錄集**物件。  
  
 *appended-column-list*  
 在其中每個項目會定義產生的父代中的資料行清單。 每個項目包含的章節資料行、 新的資料行、 導出資料行或在子系的彙總函式所產生的值**資料錄集**。  
  
 *grp-field-list*  
 資料行清單中的父和子**資料錄集**指定資料列應該如何群組子系中的物件。  
  
 中的每個資料行*grp 欄位清單*沒有對應的資料行中的子系和父系**資料錄集**物件。 每個資料列的父**資料錄集**，則*grp 欄位清單*資料行具有唯一的值和子**資料錄集**父元素所參考資料列僅包含子其資料列*grp 欄位清單*資料行具有相同的父資料列的值。  
  
 如果包含，BY 子句，則子系**資料錄集**的資料列會根據使用的計算子句中的資料行分組。 父代**Recordset**會包含每個群組的子系中的資料列的一個資料列**資料錄集**。  
  
 如果省略 BY 子句，則將整個子**Recordset**會被視為單一群組和父代**資料錄集**會包含一個資料列。 該資料列將會參考整個子系**資料錄集**。 省略 BY 子句可讓您透過將整個子計算 「 總計 」 彙總**資料錄集**。  
  
 例如：  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 不論哪種方式父**Recordset**形成 （使用計算或使用附加），它會包含用來使它關聯的子系的章節資料行**資料錄集**。 如果您想要父代**資料錄集**也可能包含子資料列包含彙總 （SUM、 MIN、 MAX 和等等） 的資料行。 父和子系**資料錄集**可能包含資料行包含在中的資料列的運算式**資料錄集**，以及資料行的新和一開始空白。  
  
## <a name="operation"></a>運算  
 *子命令*發給的提供者傳回的子系**資料錄集**。  
  
 COMPUTE 子句中指定的父資料行**Recordset**，這可能是子系參考**資料錄集**，一或多個彙總、 計算的運算式或新的資料行。 包含 BY 子句時，它所定義的資料行也會附加至父代**資料錄集**。 BY 子句會指定如何在子系的資料列**資料錄集**分組。  
  
 例如，假設您有一個資料表，名為人口統計資料，其中包含狀態、 縣 （市），以及擴展的欄位。 （母體擴展中的數字的資料表會提供僅做為範例。）  
  
|State|[縣/市]|母體|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|或|Medford|200,000|  
|或|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|聖地牙哥|600,000|  
|WA|Tacoma|500,000|  
|或|Corvallis|300,000|  
  
 現在，發出此圖形的命令：  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 此命令會開啟形狀**資料錄集**具有兩個層級。 父層級會產生**資料錄集**彙總的資料行 (`SUM(rs.population)`)、 資料行參考子系**資料錄集**(`rs`)，並加入資料行來分組子**Recordset** (`state`)。 子層級時**Recordset**查詢命令傳回 (`select * from demographics`)。  
  
 子系**資料錄集**詳細資料列會依狀態分組否則不依特定順序。 也就是群組將無法以字母或數字的順序。 如果您想要的父**資料錄集**經過排序，您可以使用**排序資料錄集**方法來排序父**資料錄集**。  
  
 您現在可以瀏覽開啟的父**Recordset**並存取子的詳細資料**資料錄集**物件。 如需詳細資訊，請參閱 <<c0> [ 存取階層式資料錄集中的資料列](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)。  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>結果的父系和子系的詳細資料錄集  
  
### <a name="parent"></a>父系  
  
|SUM (rs。母體擴展）|rs|State|  
|---------------------------|--------|-----------|  
|1,300,000|Child1 參考|CA|  
|1,200,000|Child2 參考|WA|  
|1,100,000|Child3 參考|或|  
  
## <a name="child1"></a>Child1  
  
|State|[縣/市]|母體|  
|-----------|----------|----------------|  
|CA|Los Angeles|800,000|  
|CA|聖地牙哥|600,000|  
  
## <a name="child2"></a>Child2  
  
|State|[縣/市]|母體|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|WA|Tacoma|500,000|  
  
## <a name="child3"></a>Child3  
  
|State|[縣/市]|母體|  
|-----------|----------|----------------|  
|或|Medford|200,000|  
|或|Portland|400,000|  
|或|Corvallis|300,000|  
  
## <a name="see-also"></a>另請參閱  
 [存取階層式資料錄集中的資料列](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [資料成形概觀](../../../ado/guide/data/data-shaping-overview.md)   
 [Field 物件](../../../ado/reference/ado-api/field-object.md)   
 [正式 Shape 文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [資料成形所需的提供者](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [一般 shape 命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [Value 屬性 (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic for Applications 函式](../../../ado/guide/data/visual-basic-for-applications-functions.md)
