---
title: 多維度架構和資料的總覽 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e4681bb9e1fd1028ee1ddc2bd7f72efc03fb6c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923182"
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>多維度結構描述和資料的概觀
## <a name="understanding-multidimensional-schemas"></a>瞭解多維度架構  
 ADO MD 中的中央中繼資料物件是*cube*，其中包含一組結構化的相關維度、階層、層級和成員。  
  
 「*維度*」（dimension）是從您的商業實體衍生而來的獨立資料類別，來自多維度資料庫。 維度通常會包含要當做資料庫量值之查詢準則使用的專案。  
  
 階層*是維度*匯總的路徑。 維度可能有多個資料細微性層級，其具有父子式關聯性。 階層會定義這些層級的關聯方式。  
  
 *層級*是階層中匯總的步驟。 針對具有多個資訊層的維度，每一層都是層級。  
  
 「*成員*」是維度中的資料項目。 通常，您會建立標題，或使用成員來描述資料庫的量值。  
  
 Cube 是由 ADO MD 中的[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)物件表示。 維度[、階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)、層級和成員也會以其對應的 ADO MD 物件來表示：[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)、階層、[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)和[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)。  
  
### <a name="dimensions"></a>維度  
 Cube 的維度取決於您的商務實體，以及要在資料庫中模型化的資料類型。 一般而言，每個維度都是一個獨立的進入點或用來選取資料的機制。  
  
 例如，包含銷售資料的 cube 具有下列五個維度：銷售人員、地理位置、時間、產品和量值。 [量值] 維度包含實際的銷售資料值，而其他維度則代表分類和分組銷售資料值的方式。  
  
 Geography 維度具有下列成員集：  
  
```console
{All, North America, Europe, Canada, USA, UK, Germany, Canada-West,  
Canada-East, USA-NW, USA-SW, USA-NE, USA-SE, England, Scotland,   
Wales,Ireland, Germany-North, Germany-South, Ottawa, Toronto,   
Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston,   
Shreveport, Miami, Boston, New York, London, Dover, Glasgow,   
Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin,   
Hamburg, Munich, Stuttgart}  
```  
  
### <a name="hierarchies"></a>階層  
 階層會定義維度層級可以「匯總」或群組的方式。 一個維度可以有一個以上的階層。 「地理位置」維度中存在自然階層：  
  
### <a name="levels"></a>Levels  
 在上圖中所示的 [地理位置] 維度範例中，每個方塊都代表階層中的層級。  
  
 每個層級都有一組成員，如下所示：  
  
-   世界`= {All}`  
  
-   大陸`= {North America, Europe}`  
  
-   參與者`= {Canada, USA, UK, Germany}`  
  
-   各地`= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   城市`= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>成員  
 階層分葉層級的成員沒有子系，且根層級的成員沒有父系。 所有其他成員至少有一個父系和至少一個子系。 例如，Geography 維度中階層樹狀結構的部分遍歷會產生下列父子式關聯性：  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 成員可以根據每個維度合併一或多個階層。 假設有一個時間維度，其中有兩種方式可從日層級匯總至 Year 層級：  
  
 這個範例也會說明另一個特性： Year 周階層的周層級的某些成員不會出現在年季階層的任何層級中。 因此，階層不需要包含維度的所有成員。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多維度）（ADO MD）](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [使用 ADO MD 進行程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO 搭配 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [使用多維度資料](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
