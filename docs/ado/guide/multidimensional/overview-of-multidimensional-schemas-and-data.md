---
title: 多維度的結構描述和資料的概觀 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70bd6f1867d48a9c96f5759d95c2a08a22714d8a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811156"
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>多維度結構描述和資料的概觀
## <a name="understanding-multidimensional-schemas"></a>了解多維度的結構描述  
 中央中繼資料物件，在 ADO MD *cube*，後者包含一組結構化相關的維度、 階層、 層級和成員。  
  
 A*維度*是獨立的類別，將資料從多維度資料庫，衍生自您的商務實體。 維度通常會包含做為資料庫的量值的查詢準則的項目。  
  
 A*階層*是維度的彙總的路徑。 維度可能有多個層級的資料粒度，具有父子式關聯性。 階層會定義這些層級的關聯方式。  
  
 A*層級*是階層中的彙總的步驟。 維度的多層，每個圖層會是資訊的層級。  
  
 A*成員*是維度中的資料項目。 一般而言，您建立標題或描述的資料庫使用成員的量值。  
  
 Cube 由[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)中 ADO MD 物件 維度、 階層、 層級和成員也都表示其相對應的 ADO MD 物件：[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)，[階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)，[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)，和[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)。  
  
### <a name="dimensions"></a>維度  
 Cube 的維度，取決於您的商務實體和類型的資料進行模型化資料庫中。 一般而言，每個維度是獨立的進入點或選取資料的機制。  
  
 例如，包含銷售資料的 cube 有下列五個維度： 銷售人員、 地理位置、 時間、 產品和量值。 此量值維度包含實際的銷售資料值，而其他維度代表分類及分組的銷售資料值的方式。  
  
 [Geography] 維度具有下列成員的集合：  
  
```  
{All, North America, Europe, Canada, USA, UK, Germany, Canada-West,  
Canada-East, USA-NW, USA-SW, USA-NE, USA-SE, England, Scotland,   
Wales,Ireland, Germany-North, Germany-South, Ottawa, Toronto,   
Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston,   
Shreveport, Miami, Boston, New York, London, Dover, Glasgow,   
Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin,   
Hamburg, Munich, Stuttgart}  
```  
  
### <a name="hierarchies"></a>階層  
 階層會定義所在之維度的層級可以是 「 積存 」 或分組的方式。 維度可能會有一個以上的階層。 自然階層存在於 [Geography] 維度：  
  
### <a name="levels"></a>Levels  
 在上圖中顯示範例 Geography 維度中，每個方塊都代表階層中的層級。  
  
 每個層級具有一組成員，如下所示：  
  
-   世界 `= {All}`  
  
-   各大洲 `= {North America, Europe}`  
  
-   國家/地區 `= {Canada, USA, UK, Germany}`  
  
-   區域 `= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   城市 `= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>成員  
 在階層的分葉層級的成員有任何子節點，及根層級的成員具有沒有父代。 所有其他成員都有至少一個父代和至少一個子系。 例如，Geography 維度階層樹狀結構的部分周遊，就會產生下列的父子式關聯性：  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 可以沿著每個維度的一個或多個階層合併成員。 請考慮時間維度有兩種方式可從天層級彙總 Year 層級：  
  
 此範例也說明了另一個特性： 年度季階層的任何層級中看不到一週的階層層級年週的某些成員。 因此，階層不需要包含維度的所有成員。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多維度） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [使用 ADO MD 進行程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO MD 使用 ADO](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [使用多維度資料](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
