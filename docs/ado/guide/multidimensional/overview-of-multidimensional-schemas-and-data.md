---
title: "多維度結構描述和資料的概觀 |Microsoft 文件"
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
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cf3e8d6bebd5860df9f52236eecf4d1f287a8f9d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="overview-of-multidimensional-schemas-and-data"></a>多維度結構描述和資料的概觀
## <a name="understanding-multidimensional-schemas"></a>了解多維度結構描述  
 在 ADO MD 中的中央中繼資料物件是*cube*，其中包含的一組結構化相關的維度、 階層、 層級和成員。  
  
 A*維度*是多維度資料庫，衍生自您的商務實體資料的獨立類別目錄。 維度通常會包含要做為資料庫的量值的查詢準則的項目。  
  
 A*階層*是維度的彙總的路徑。 維度可能有多個層級的資料粒度，具有父子式關聯性。 階層會定義這些層級的關聯方式。  
  
 A*層級*是階層中的彙總的步驟。 對於具有多個圖層的維度，每個圖層會是資訊的層級。  
  
 A*成員*維度中的資料項目。 一般而言，您建立標題或描述資料庫使用成員的量值。  
  
 Cube 由[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) ADO MD 中的物件 維度、 階層、 層級和成員也由其對應的 ADO MD 物件表示：[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)，[階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)，[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)，和[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)。  
  
### <a name="dimensions"></a>維度  
 Cube 的維度取決於您的商務實體以及要在資料庫中建立模型的資料類型。 一般而言，每個維度是獨立的進入點或選取資料的機制。  
  
 例如，包含銷售資料的 cube 有下列五種維度： 銷售人員、 地理位置、 時間、 產品與量值。 此量值維度包含實際的銷售資料值，其他維度則代表以分類和分組的銷售資料值的方式。  
  
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
 階層定義所在之維度的層級可以是 「 積存 」 或分組的方式。 維度可能會有一個以上的階層。 [Geography] 維度中，有自然階層：  
  
### <a name="levels"></a>Levels  
 在上圖中顯示範例 Geography 維度中，每個方塊都代表階層中的層級。  
  
 每個層級具有一組成員，如下所示：  
  
-   世界`= {All}`  
  
-   大陸`= {North America, Europe}`  
  
-   國家 （地區)`= {Canada, USA, UK, Germany}`  
  
-   區域`= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   城市`= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>成員  
 在階層的分葉層級的成員沒有子系，且在根層級的成員具有沒有父代。 所有其他成員都有至少一個父系類別與至少一個子系。 例如，Geography 維度的階層樹狀結構的部分周遊會產生下列的父子式關聯性：  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 可以沿著每個維度的一個或多個階層合併成員。 時間維度，請考慮在有兩種方式可從天層級彙總年層級：  
  
 此範例也會說明其他特性： 週的階層層級年週的某些成員不會出現在年度季階層的任何層級。 因此，階層不需要包含維度的所有成員。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多維度） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [使用 ADO MD 程式設計](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO 搭配 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [使用多維度資料](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
