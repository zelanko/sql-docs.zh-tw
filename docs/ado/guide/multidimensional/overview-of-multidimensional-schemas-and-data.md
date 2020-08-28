---
description: 多維度結構描述和資料的概觀
title: 多維度架構和資料的總覽 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
author: rothja
ms.author: jroth
ms.openlocfilehash: 431ff25d49c4a45055d796aba98f229564872a4e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978639"
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>多維度結構描述和資料的概觀
## <a name="understanding-multidimensional-schemas"></a>瞭解多維度架構  
 ADO MD 中的中央中繼資料物件是 *cube*，其中包含一組結構化的相關維度、階層、層級和成員。  
  
 維度是來自您的多 *維度* 資料庫之資料的獨立類別，衍生自您的商務實體。 維度通常包含要當做資料庫量值查詢準則使用的專案。  
  
 階層 *是維度* 匯總的路徑。 維度可能有多個層級的資料細微性，其具有父子式關聯性。 階層定義這些層級的關聯方式。  
  
 *層級*是階層中匯總的步驟。 針對具有多層資訊的維度，每一層都是層級。  
  
 *成員*是維度中的資料項目。 一般而言，您會使用成員建立標題或描述資料庫的量值。  
  
 Cube 是由 ADO MD 中的 [CubeDef](../../reference/ado-md-api/cubedef-object-ado-md.md) 物件表示。 維度、階層、層級和成員也會以對應的 ADO MD 物件表示： [維度](../../reference/ado-md-api/dimension-object-ado-md.md)、 [階層](../../reference/ado-md-api/hierarchy-object-ado-md.md)、 [層級](../../reference/ado-md-api/level-object-ado-md.md)和 [成員](../../reference/ado-md-api/member-object-ado-md.md)。  
  
### <a name="dimensions"></a>維度  
 Cube 的維度取決於您的商務實體和要在資料庫中建立模型的資料類型。 一般而言，每個維度都是一個獨立的進入點，也就是選取資料的機制。  
  
 例如，包含銷售資料的 cube 具有下列五個維度：銷售人員、地理位置、時間、產品和量值。 量值維度包含實際的銷售資料值，而其他維度則代表分類和分組銷售資料值的方式。  
  
 Geography 維度有下列成員集合：  
  
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
 階層定義維度層級可以「匯總」或群組的方式。 維度可以有一個以上的階層。 [Geography] 維度中有一個自然階層：  
  
### <a name="levels"></a>等級  
 在上圖所示的 [地理位置] 維度範例中，每個方塊都代表階層中的層級。  
  
 每個層級都有一組成員，如下所示：  
  
-   世界 `= {All}`  
  
-   大洲 `= {North America, Europe}`  
  
-   國家 `= {Canada, USA, UK, Germany}`  
  
-   地區 `= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   城市 `= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>成員  
 階層的分葉層級的成員沒有子系，而且根層級的成員沒有父系。 所有其他成員都至少有一個父系和至少一個子系。 例如，地理位置維度中階層樹狀結構的部分遍歷會產生下列父子式關聯性：  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 成員可以沿著每個維度的一或多個階層合併。 假設有兩種時間維度可從日層級匯總至年度層級：  
  
 此範例也會說明另一個特性：年份階層中，周層級的某些成員不會出現在年度季階層的任何層級中。 因此，階層不需要包含維度的所有成員。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../reference/ado-md-api/ado-md-object-model.md)   
 [ADO (多維度)  (ADO MD) ](./ado-multidimensional-ado-md.md)   
 [使用 ADO MD 進行程式設計](./programming-with-ado-md.md)   
 [使用 ADO 搭配 ADO MD](./using-ado-with-ado-md.md)   
 [使用多維度資料](./working-with-multidimensional-data.md)