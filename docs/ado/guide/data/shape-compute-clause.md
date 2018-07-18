---
title: 圖形 COMPUTE 子句 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 183d6536d5202c9795837a4e35f740753b77703f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272827"
---
# <a name="shape-compute-clause"></a>圖形 COMPUTE 子句
圖形 COMPUTE 子句產生父代**資料錄集**，其資料行所組成之子系的參考**資料錄集**; 選擇性資料行內容的章節中，新的、 或導出資料行，或子系上執行彙總函式的結果**資料錄集**或先前形狀**資料錄集**; 以及從子系的任何資料行**資料錄集**中所列選擇性的 BY 子句。  
  
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
  
-   查詢命令，在大括號 ("{}")，則會傳回子**資料錄集**物件。 命令發行至基礎資料提供者，並且它的語法取決於該提供者的需求。 這通常會是 SQL 語言，雖然 ADO 不需要任何特殊的查詢語言。  
  
-   現有的形狀名稱**資料錄集**。  
  
-   另一個圖形的命令。  
  
-   資料表關鍵字，後面接著資料提供者中的資料表名稱。  
  
 *child-alias*  
 用來參考別名**資料錄集**傳回*子命令。* *子別名*COMPUTE 子句中的資料行清單中必要參數，定義父系和子系之間的關聯性**資料錄集**物件。  
  
 *appended-column-list*  
 在其中每個項目定義產生的父代中的資料行清單。 每個項目包含的章節資料行、 新的資料行、 導出資料行或所產生的子系上的彙總函式值**資料錄集**。  
  
 *grp-field-list*  
 父系和子系中的資料行清單**資料錄集**指定資料列應該如何群組之子系的物件。  
  
 每個資料行中*群組欄位清單，* 沒有對應的資料行中的子系和父系**資料錄集**物件。 每個資料列的父**資料錄集**、*群組欄位清單*資料行具有唯一的值與子系**資料錄集**參考的父資料列僅包含子資料列的*群組欄位清單*資料行具有與父資料列相同的值。  
  
 如果包含，BY 子句，則子系**資料錄集**的資料列會根據 COMPUTE 子句中的資料行群組。 父代**資料錄集**會包含一個資料列的每一個子系中的資料列群組**資料錄集**。  
  
 如果省略 BY 子句，則整個子系**資料錄集**會被視為單一群組和父代**資料錄集**會包含一個資料列。 該資料列將會參考整個子系**資料錄集**。 省略 BY 子句可讓您透過整個子系計算 「 總計 」 彙總**資料錄集**。  
  
 例如：  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 不論哪種方式父**資料錄集**形成 （使用計算或使用附加），它會包含用來關聯至子系的章節資料行**資料錄集**。 如果您想，父系**資料錄集**也可能包含透過子資料列包含彙總 （SUM、 MIN、 MAX 和等等） 的資料行。 父和子系**資料錄集**可能包含資料行包含在中的資料列的運算式**資料錄集**，以及空的資料行，新的和一開始。  
  
## <a name="operation"></a>作業  
 *子命令*發行給提供者，則會傳回子**資料錄集**。  
  
 COMPUTE 子句指定的父資料行**資料錄集**，這可能是子系的參考**資料錄集**，一或多個彙總、 計算的運算式或新的資料行。 如果沒有包含 BY 子句，它定義的資料行也會附加至父**資料錄集**。 BY 子句會指定如何在子系的資料列**資料錄集**分組。  
  
 例如，假設您有一個資料表，名為人口統計資料，包括狀態、 縣市和母體擴展的欄位。 （僅做為範例會提供圖形內資料表的母體擴展。）  
  
|State|[縣/市]|母體|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|或|Medford|200,000|  
|或|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|聖地牙哥|600,000|  
|WA|Tacoma|500,000|  
|或|Corvallis|300,000|  
  
 現在，發出此圖形命令：  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 此命令會開啟形狀**資料錄集**與兩個層級。 父層級會產生**資料錄集**與彙總的資料行 (`SUM(rs.population)`)、 參考子系的資料行**資料錄集**(`rs`)，並加入資料行來分組子**資料錄集**(`state`)。 子層級是**資料錄集**查詢命令傳回 (`select * from demographics`)。  
  
 子系**資料錄集**詳細資料列將會依狀態分組否則不依特定順序。 也就是以字母或數字順序不會有群組。 如果您想父**資料錄集**才能建立此順序，您可以使用**資料錄集排序**方法來排序父**資料錄集**。  
  
 您現在可以瀏覽開啟的父**資料錄集**存取子的詳細資料和**資料錄集**物件。 如需詳細資訊，請參閱[存取階層式資料錄集中的資料列](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)。  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>結果的父系和子詳細資料錄集  
  
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
 [存取資料列中的階層式資料錄集](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [資料成形概觀](../../../ado/guide/data/data-shaping-overview.md)   
 [Field 物件](../../../ado/reference/ado-api/field-object.md)   
 [型式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [提供者所需的資料成形](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [圖形 APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [在一般的圖形命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [Value 屬性 (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic for Applications 函式](../../../ado/guide/data/visual-basic-for-applications-functions.md)
