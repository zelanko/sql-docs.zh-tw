---
title: "圖案的一般命令 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 245f842883ec0be1ac92ad58ea75b4cdef7d9cb3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="shape-commands-in-general"></a>在一般的圖形命令
資料成形定義的資料行的形狀**資料錄集**，資料行中的方式所表示的實體之間的關聯性**資料錄集**已填入資料。  
  
 形狀**資料錄集**可以包含下列類型的資料行。  
  
|資料行類型|Description|  
|-----------------|-----------------|  
|data|從欄位**資料錄集**資料提供者傳回的查詢命令，資料表，或先前形狀**資料錄集**。|  
|本文章節|另一個的參考**資料錄集**，稱為*章*。 章節資料行讓您定義*父子式*關聯性其中*父*是**資料錄集**包含章節資料行和*子*是**資料錄集**本章所表示。|  
|彙總 (aggregate)|資料行的值由執行*彙總函式*上的所有資料列或子系的所有資料列的資料行**資料錄集**。 (請參閱下列主題中的彙總函式[彙總函式、 CALC 函式和 NEW 關鍵字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)。)|  
|計算的運算式|計算在 Visual Basic 應用程式中的相同資料列的資料行的運算式衍生的資料行值**資料錄集**。 運算式會計算函數的引數。 (請參閱下列主題中的計算運算式[彙總函式、 CALC 函式和 NEW 關鍵字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)和[應用程式函式的 Visual Basic](../../../ado/guide/data/visual-basic-for-applications-functions.md)。)|  
|new|空白、 優質 欄位，它可以在稍後以資料擴展。 資料行定義新的關鍵字。 (請參閱下列主題中的新關鍵字[彙總函式、 CALC 函式和 NEW 關鍵字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)。)|  
  
 Shape 命令可以包含一個子句，指定將會傳回基礎資料提供者的查詢命令**資料錄集**物件。 查詢的語法取決於基礎資料提供者的需求。 這通常是語言的 SQL，雖然 ADO 不需要使用任何特定查詢。  
  
 圖形命令可以由發出**資料錄集**物件，或藉由設定[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性[命令](../../../ado/reference/ado-api/command-object-ado.md)物件，然後再呼叫[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法。  
  
 您可以使用具有 SQL JOIN 子句來關聯兩個資料表。不過，一個階層式**資料錄集**可以更有效率地代表的資訊。 每個資料列的**資料錄集**另外從一個資料表聯結的重複資訊所建立。 階層式**資料錄集**只有一個父**資料錄集**每多個子**資料錄集**物件。  
  
 圖形命令可以巢狀化。 也就是說，*父命令*或*子命令*本身可能是另一個圖形的命令。  
  
 Shape 提供者一律會傳回用戶端資料指標，即使使用者指定的資料指標位置**adUseServer**。  
  
 您可以存取**資料錄集**元件形狀**資料錄集**以程式設計方式或透過適當的視覺控制項。  
  
 Microsoft 提供視覺化工具，會產生圖形命令 (請參閱[資料環境設計師](http://go.microsoft.com/fwlink/?LinkId=5689)Visual Basic 6 文件中) 和另一個則會顯示 （請參閱 「 使用 Microsoft 階層的階層式資料指標Flexgrid 控制項 」 中的 Visual Basic 6 文件）。  
  
 如需有關瀏覽階層式資訊**資料錄集**，請參閱[存取階層式資料錄集中的資料列](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)。  
  
 精確語法正確的圖形命令的詳細資訊，請參閱[正式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)。  
  
 此章節包含下列主題。  
  
-   [彙總函式、 CALC 函式和 NEW 關鍵字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [發出命令至基礎資料提供者](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)

