---
description: 資料成形範例
title: 資料成形範例 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
author: rothja
ms.author: jroth
ms.openlocfilehash: b6d6310e27db65576aac3ed79e699200dfa31c18
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991439"
---
# <a name="data-shaping-example"></a>資料成形範例
下列資料成形命令示範如何從 Northwind 資料庫的**Customers**和**Orders**資料表建立階層式**記錄集**。  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 當此命令用來開啟**記錄集**物件時 (如[Visual Basic 的資料成形) 範例](./visual-basic-example-of-data-shaping.md)所示，它會為**Customers**資料表所傳回的每一筆記錄建立 (**chapOrders**) 的章節。 本章包含從**Orders**資料表傳回之**記錄集**的子集。 **ChapOrders**章節包含有關指定客戶所下訂單的所有要求資訊。 在此範例中，章節包含三個數據行： [ **訂單 id**]、[ **訂購日期**] 和 [ **CustomerID**]。  
  
 結果成形 **記錄集** 的前兩個專案如下所示：  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 在 SHAPE 命令中，APPEND 會用來建立與父**記錄集**相關的子**記錄集**， (在 [關聯] 子句稍) 早所討論的 SHAPE 關鍵字之後，從提供者特定的命令傳回。 父系和子系通常至少有一個共通的資料行：父項的資料列中的資料行值與子系中所有資料列的資料行值相同。  
  
 有第二種方式可使用 SHAPE 命令：亦即，從子**記錄集**產生父**記錄集**。 子 **記錄集中** 的記錄會分組（通常是使用 by 子句），而且會針對子系中每個產生的群組，將一個資料列加入至父 **記錄集** 。 如果省略 BY 子句，子 **記錄集會** 形成單一群組，且父 **記錄集** 將只包含一個資料列。 這對於計算整個子 **記錄集**的「總計」匯總很有用。  
  
 SHAPE 命令結構也可讓您以程式設計方式建立已成形的 **記錄集**。 然後，您可以透過程式設計方式或透過適當的視覺控制項來存取 **記錄集** 的元件。 Shape 命令的發出方式就像任何其他 ADO 命令文字一樣。 如需詳細資訊，請參閱 [一般圖形命令](./shape-commands-in-general.md)。  
  
 無論父 **記錄集** 的形成方式為何，它都會包含用來將它與子 **記錄集**相關聯的章節資料行。 如果您想要的話，父 **記錄集** 也可以有資料行包含匯總 (SUM、MIN、MAX 等等) 子資料列。 父 **記錄集和子記錄集** 都可以有資料行包含 **記錄集**內資料列上的運算式，以及新的和一開始是空的資料行。  
  
 本節將繼續進行下列主題。  
  
-   [Visual Basic 的資料成形範例](./visual-basic-example-of-data-shaping.md)