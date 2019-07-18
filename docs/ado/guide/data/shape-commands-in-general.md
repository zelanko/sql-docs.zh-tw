---
title: 圖形的一般命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 09fec8bd07d036fd6a93b8f6bcb54a51a68150fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924170"
---
# <a name="shape-commands-in-general"></a>一般 Shape 命令
資料成形定義形狀的資料行**Recordset**，資料行中的方式所表示的實體之間的關聯性**資料錄集**已填入資料。  
  
 形狀**資料錄集**可以包含下列類型的資料行。  
  
|資料行類型|描述|  
|-----------------|-----------------|  
|data|從欄位**Recordset**資料提供者傳回的查詢命令，資料表，或先前形狀**資料錄集**。|  
|章節|另一個的參考**Recordset**，稱為*章*。 章節資料行會使您能夠定義*父系-子系*關聯性其中*父系*會**資料錄集**包含章節資料行和*子系*是**資料錄集**一章所表示。|  
|彙總 (aggregate)|資料行的值藉由執行衍生*彙總函式*上的所有資料列或子系的所有資料列的資料行**資料錄集**。 (請參閱下列主題中的彙總函式[彙總函式、 CALC 函式和 NEW 關鍵字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)。)|  
|導出的運算式|資料行的值衍生的計算方式 Visual Basic 應用程式中的相同資料列的資料行的運算式**資料錄集**。 運算式是 CALC 函式的引數。 (請參閱下列主題中的計算運算式[彙總函式、 CALC 函式和 NEW 關鍵字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)然後在[Visual Basic for Applications 函式](../../../ado/guide/data/visual-basic-for-applications-functions.md)。)|  
|new|空的製作欄位，而這可以在稍後以資料擴展。 新的關鍵字來定義資料行。 (請參閱下列主題中的新關鍵字[彙總函式、 CALC 函式和 NEW 關鍵字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)。)|  
  
 Shape 命令可以包含指定的查詢命令，以將會傳回基礎資料提供者的子句**資料錄集**物件。 查詢的語法取決於基礎資料提供者的需求。 這通常是 SQL，雖然 ADO 不需要使用任何特定的查詢語言。  
  
 可以藉由發出圖形命令**資料錄集**物件，或藉由設定[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性[命令](../../../ado/reference/ado-api/command-object-ado.md)物件，然後再呼叫[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法。  
  
 您可以使用的 SQL JOIN 子句來關聯兩個資料表;不過，階層**資料錄集**可以更有效率地表示的資訊。 每個資料列**資料錄集**建立重複的其中一個資料表的聯結重複項目資訊。 階層式**資料錄集**只有一個父代**資料錄集**針對每個多個子**資料錄集**物件。  
  
 可以是巢狀圖形命令。 亦即*父命令*或是*子命令*本身可能是另一個圖形的命令。  
  
 Shape 提供者一律會傳回用戶端資料指標，即使在使用者指定的資料指標位置時，才**adUseServer**。  
  
 您可以存取**Recordset**元件的形狀**資料錄集**以程式設計方式或透過適當的視覺控制項。  
  
 Microsoft 提供一種視覺化工具，會產生圖形命令 (請參閱[資料環境設計師](https://go.microsoft.com/fwlink/?LinkId=5689)Visual Basic 6 文件中)，另一個則會顯示 （請參閱 「 使用 Microsoft 階層的階層式資料指標Flexgrid 控制項 」 中的 Visual Basic 6 文件）。  
  
 如需有關瀏覽階層式資訊**Recordset**，請參閱[存取階層式資料錄集中的資料列](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)。  
  
 精確語法正確的圖形命令的詳細資訊，請參閱[正式 Shape 文法](../../../ado/guide/data/formal-shape-grammar.md)。  
  
 此章節包含下列主題。  
  
-   [彙總函式、CALC 函式和 NEW 關鍵字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [發出命令給基礎資料提供者](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
