---
description: 一般 Shape 命令
title: 一般圖形命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
author: rothja
ms.author: jroth
ms.openlocfilehash: c20132fe933d232d38ee843a706e9ad923d0d376
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724929"
---
# <a name="shape-commands-in-general"></a>一般 Shape 命令
資料成形定義了成形 **記錄集**的資料行、資料行所代表的實體之間的關聯性，以及 **記錄集** 填入資料的方式。  
  
 成形的 **記錄集** 可由下列類型的資料行組成。  
  
|資料行類型|描述|  
|-----------------|-----------------|  
|資料|從查詢命令所傳回之 **記錄集** 的欄位，到資料提供者、資料表或先前成形的 **記錄集**。|  
|章|另一個 **記錄集**的參考，稱為「 *章節*」。 章節資料行可讓您定義 *父子式* 關聯性，其中 *父系* 是包含章節資料行的 **記錄集** ，而 *子* 系是該章節所代表的 **記錄集** 。|  
|彙總 (aggregate)|資料行的值是藉由在所有資料列或子**記錄集**之所有資料列的資料行上執行*彙總函式*所衍生。  (請參閱下列主題中的彙總函式、 [彙總函式、CALC 函式和 NEW 關鍵字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)。 ) |  
|計算運算式|資料行的值是藉由計算 **記錄集**相同資料列中資料行的 Visual Basic for Applications 運算式所衍生。 運算式是 CALC 函數的引數。  (參閱下列主題中的計算運算式、 [彙總函式、CALC 函式和 NEW 關鍵字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md) 以及 In [Visual Basic for Applications 函數](../../../ado/guide/data/visual-basic-for-applications-functions.md)。 ) |  
|new|空白的製造欄位，可在稍後填入資料。 此資料行是以 NEW 關鍵字定義。  (在下列主題中看到 NEW 關鍵字、 [彙總函式、CALC 函式和 New 關鍵字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)。 ) |  
  
 Shape 命令可以包含子句，此子句會指定查詢命令給將傳回 **記錄集** 物件的基礎資料提供者。 查詢的語法取決於基礎資料提供者的需求。 雖然 ADO 不需要使用任何特定的查詢語言，但這通常會是 SQL。  
  
 Shape 命令可以由**記錄集**物件發出，或藉由設定[Command](../../../ado/reference/ado-api/command-object-ado.md)物件的[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性，然後呼叫[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法來發出。  
  
 您可以使用 SQL JOIN 子句來建立兩個數據表的關聯;不過，階層式 **記錄集** 可以更有效率地表示資訊。 聯結所建立之 **記錄集** 的每個資料列都會重複來自其中一個資料表的資訊。 階層式**記錄**集的每個子**記錄集**物件只有一個父**記錄集**。  
  
 Shape 命令可以進行嵌套。 也就是說， *父系命令* 或 *子命令* 本身可能是另一個圖形命令。  
  
 圖形提供者一律會傳回用戶端資料指標，即使使用者指定 **adUseServer**的資料指標位置也一樣。  
  
 您可以透過程式設計方式或透過適當的視覺控制項來存取成形**記錄集**的**記錄集**元件。  
  
 Microsoft 提供的視覺化檢視會產生圖形命令 (請參閱 Visual Basic 6 檔) 中的 [資料環境設計](/previous-versions/visualstudio/aa445793(v=vs.60)) 工具，以及顯示階層式資料指標的另一項， (在 Visual Basic 6 檔) 中看到「使用 Microsoft 階層式 Flexgrid 控制項」。  
  
 如需導覽階層式 **記錄集**的詳細資訊，請參閱 [存取階層式記錄](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)集中的資料列。  
  
 如需語法正確之圖形命令的精確資訊，請參閱 [正式形式的文法](../../../ado/guide/data/formal-shape-grammar.md)。  
  
 此章節包含下列主題。  
  
-   [彙總函式、CALC 函式和 NEW 關鍵字](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [發出命令給基礎資料提供者](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)