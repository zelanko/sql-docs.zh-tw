---
title: 資料成形範例 |Microsoft 文件
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
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32001c7f0a9ceff2fdccdf6d0bd0902b345f2a68
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271387"
---
# <a name="data-shaping-example"></a>資料成形範例
下列資料成形命令示範如何建置階層式**資料錄集**從**客戶**和**訂單**Northwind 資料庫中的資料表。  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 此命令用來開啟**資料錄集**物件 (如中所示[Visual Basic 範例的資料成形](../../../ado/guide/data/visual-basic-example-of-data-shaping.md))，它會建立一個章節 (**chapOrders**) 傳回每一筆記錄從**客戶**資料表。 本章所組成的子集**資料錄集**從傳回**訂單**資料表。 **ChapOrders**章節包含特定客戶所下訂單的所有要求的資訊。 此範例中，在本章包含三個資料行： **OrderID**， **OrderDate**，和**CustomerID**。  
  
 產生的形狀的前兩個項目**資料錄集**如下：  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 在圖形命令中，新增用來建立子系**資料錄集**與父系相關**資料錄集**（如同先前討論的內容的圖形關鍵字之後，傳回提供者特定命令較早的） RELATE 子句。 父系和子系通常有至少一個資料行共同： 的父資料列中的資料行的值是做為子系的所有資料列中的資料行的值相同。  
  
 若要使用圖形命令的第二個方式： 也就是產生父代**資料錄集**從子系**資料錄集**。 中子系的記錄**資料錄集**分組，通常使用 BY 子句和一個資料列加入至父代**資料錄集**針對每個產生的群組之子系。 如果省略 BY 子句，則子系**資料錄集**可形成單一的群組和父代**資料錄集**會包含一個資料列。 這適用於 「 總計 」 彙總計算透過整個子系**資料錄集**。  
  
 圖形命令建構也可讓您以程式設計方式建立形狀**資料錄集**。 然後，您就可以存取的元件**資料錄集**以程式設計方式或透過適當的視覺控制項。 Shape 命令會發出與任何其他 ADO 命令文字相似。 如需詳細資訊，請參閱[圖案的一般命令](../../../ado/guide/data/shape-commands-in-general.md)。  
  
 不論哪種方式父**資料錄集**是正確格式，它會包含用來關聯至子系的章節資料行**資料錄集**。 如果您想，父系**資料錄集**也可以有子資料列包含彙總 （SUM、 MIN、 MAX 和等等） 的資料行。 父和子系**資料錄集**可以有包含的運算式中的資料列上的資料行**資料錄集**，以及空的資料行是在新的且一開始。  
  
 本節會繼續進行下列主題。  
  
-   [Visual Basic 的資料成形範例](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
