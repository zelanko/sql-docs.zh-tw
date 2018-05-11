---
title: 了解資料庫結構描述 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 949b4531726891e6e206fe42c11f63739b4787ee
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="understanding-the-database-schemas"></a>了解資料庫結構描述
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  結構描述產生精靈會根據 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 裡的維度和量值群組，產生主題領域資料庫反正規化關聯式結構描述。 此精靈會針對每一個維度產生關聯式資料表 (稱為維度資料表)，以便儲存維度資料，也會針對每一個量值群組產生關聯式資料表 (稱為事實資料表)，以便儲存事實資料。 精靈產生這些關聯式資料表時，會忽略連結維度、連結量值群組和伺服器時間維度。  
  
## <a name="validation"></a>驗證  
 [結構描述產生精靈] 在開始產生基礎關聯式結構描述之前，會先驗證 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cube 和維度。 如果精靈偵測到錯誤會停止，並會在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的 [工作清單] 視窗報告錯誤。 導致無法產生之錯誤的範例包括：  
  
-   擁有一個以上之索引鍵屬性的維度。  
  
-   擁有與索引鍵屬性不同之資料類型的父屬性。  
  
-   沒有量值的量值群組。  
  
-   未正確設定的變質維度或量值。  
  
-   未正確設定的 Surrogate 索引鍵，例如使用 **ScdOriginalID** 屬性類型的多個屬性，或使用 **ScdOriginalID** (未繫結到使用整數資料類型的資料行) 的屬性。  
  
## <a name="dimension-tables"></a>維度資料表  
 針對每個維度，結構描述產生精靈會產生要包含在主題領域資料庫裡的維度資料表。 維度資料表的結構，取決於設計資料表所依據之維度時的選擇。  
  
 資料行  
 針對作為維度資料表基礎之維度中每個屬性 (Attribute) 的相關聯繫結 (例如每個屬性 (Attribute) 之 **KeyColumns**、 **NameColumn**、 **ValueColumn**、 **CustomRollupColumn**、 **CustomRollupPropertiesColumn**和 **UnaryOperatorColumn** 屬性 (Property) 的繫結)，精靈會產生一個資料行。  
  
 關聯性  
 針對每個父屬性的資料行和維度資料表的主索引鍵，精靈會產生兩者之間的關聯性。  
  
 針對定義為 Cube 中之參考維度的其他每個維度資料表，精靈也會產生與主索引鍵的關聯性 (如果適用的話)。  
  
 條件約束  
 依預設，精靈會根據維度的索引鍵屬性，為每個維度資料表產生一個主索引鍵條件約束。 如果產生主索引鍵條件約束，依預設會產生另一個名稱資料行。 即使您決定不在資料庫中建立主索引鍵，仍會在資料來源檢視中建立一個邏輯主索引鍵。  
  
> [!NOTE]  
>  如果做為維度資料表之基礎的維度中，指定了一個以上的索引鍵屬性，就會發生錯誤。  
  
 翻譯  
 精靈會另外產生一個資料表，以保存需要翻譯資料行之任何屬性的已翻譯值。 精靈也會為每一種必要的語言，建立個別資料行。  
  
## <a name="fact-tables"></a>事實資料表  
 針對 Cube 中的每個量值群組，結構描述產生精靈會產生要包含在主題領域資料庫裡的一個事實資料表。 事實資料表的結構，取決於設計資料表所依據之量值群組時的選擇，以及在量值群組與任何內含維度之間建立的關聯性。  
  
 資料行  
 精靈會為每個量值產生一個資料行，不過使用 **Count** 彙總函式的量值除外。 這些量值在事實資料表中不需要有對應的資料行。  
  
 精靈也會在量值群組上，針對每個一般維度關聯性的每個資料粒度屬性資料行，產生一個資料行；也會針對與此資料表做為基礎的量值群組，有事實維度關聯性的維度之每個屬性的相關聯繫結，產生一或多個資料行 (如果適用的話)。  
  
 關聯性  
 精靈會為每個一般維度關聯性，產生從事實資料表到維度資料表之資料粒度屬性的一個關聯性。 如果資料粒度是以維度資料表的索引鍵屬性為基礎，會在資料庫和資料來源檢視中建立關聯性。 如果資料粒度是以另一個屬性為基礎，則只會在資料來源檢視中建立關聯性。  
  
 如果您在精靈中選擇產生索引，會為每一個關聯性資料行產生一個非叢集索引。  
  
 條件約束  
 不會在事實資料表上產生主索引鍵。  
  
 如果您選擇強制執行參考完整性，適用的話，則會在維度資料表和事實資料表之間產生參考完整性條件約束。  
  
 翻譯  
 針對量值群組中需要翻譯資料行的任何屬性，精靈會產生另一個資料表來保存已翻譯值。 精靈也會為每一種必要的語言，建立個別資料行。  
  
## <a name="data-type-conversion-and-default-lengths"></a>資料類型轉換和預設長度  
 在所有情況下，[結構描述產生精靈] 會忽略資料類型，不過使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **wchar** 資料類型的資料行除外。 **wchar** 資料大小會直接轉譯成 **nvarchar** 資料類型。 但是，如果使用 **wchar** 大小指定的資料行長度大於 4000 個位元組，[結構描述產生精靈] 就會產生錯誤。  
  
 如果資料項目 (例如屬性的繫結) 沒有指定的長度，則會針對資料行使用下表中所列的預設長度。  
  
|資料項目|預設長度 (位元組)|  
|---------------|------------------------------|  
|KeyColumn|50|  
|NameColumn|50|  
|CustomRollupColumn|3000|  
|CustomRollupPropertiesColumn|500|  
|UnaryOperatorColumn|1|  
  
## <a name="see-also"></a>另請參閱  
 [了解累加式產生](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)   
 [管理資料來源檢視和資料來源的變更](../../analysis-services/multidimensional-models/manage-changes-to-data-source-views-and-data-sources.md)  
  
  
