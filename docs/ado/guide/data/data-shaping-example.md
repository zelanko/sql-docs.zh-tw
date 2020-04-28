---
title: 資料成形範例 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a946329ad95a2b226f186e571152268baa5f37c3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925661"
---
# <a name="data-shaping-example"></a>資料成形範例
下列資料成形命令示範如何在 Northwind 資料庫的**Customers**和**Orders**資料表中建立階層式**記錄集**。  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 當此命令用來開啟**記錄集**物件（如[Visual Basic 的資料成形範例](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)所示）時，它會針對每個從**Customers**資料表傳回的記錄建立一個章節（**chapOrders**）。 本章包含從**Orders**資料表傳回之**記錄集**的子集。 **ChapOrders**章節包含給定客戶所下訂單的所有要求資訊。 在此範例中，章節包含三個數據行： [**訂單**]、[**訂購日期**] 和 [ **CustomerID**]。  
  
 結果成形**記錄集**的前兩個專案如下所示：  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 在 SHAPE 命令中，APPEND 是用來建立與父**記錄集**相關的子**記錄集**（如同在稍早所討論的 SHAPE 關鍵字之後立即從提供者特定的命令傳回）。 父系和子系通常至少有一個通用的資料行：父系之資料列中的資料行值，與子系中所有資料列的資料行值相同。  
  
 有第二種方式可使用圖形命令，亦即，從子**記錄集**產生父**記錄集**。 子**記錄集**內的記錄會進行分組，通常是使用 by 子句，而一個資料列會加入至子系中每個產生之群組的父**記錄集**。 如果省略 BY 子句，子**記錄集**就會形成單一群組，而父**記錄集**只會包含一個資料列。 這適用于計算整個子**記錄集**的「總計」匯總。  
  
 圖形命令結構也可讓您以程式設計方式建立成形的**記錄集**。 接著，您可以透過程式設計方式或適當的視覺效果控制項來存取**記錄集**的元件。 圖形命令的發出方式就像任何其他 ADO 命令文字一樣。 如需詳細資訊，請參閱[一般的圖形命令](../../../ado/guide/data/shape-commands-in-general.md)。  
  
 無論父**記錄集**的形成方式為何，它都會包含一個章節資料行，用來將它與子**記錄集**產生關聯。 如果您想要的話，父**記錄集**也可以有資料行包含子資料列上的匯總（加總、最小、最大值等等）。 父系和子**記錄集**都可以有資料行，其中包含**記錄集**內資料列的運算式，以及新的和最初是空的資料行。  
  
 本節會繼續進行下列主題。  
  
-   [Visual Basic 的資料成形範例](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
