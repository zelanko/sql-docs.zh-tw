---
title: 內容類型 （資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- columns [data mining], content types
- KEY SEQUENCE column
- content types [data mining]
- attributes [data mining]
- DISCRETIZED column
- CONTINUOUS column
- CYCLICAL column
- ORDERED column
- discretized columns [data mining]
- discrete columns [Analysis Services]
- DISCRETE column
- KEY column
- KEY TIME column
- continuous columns
- coding [Data Mining]
ms.assetid: 2dacd968-70e8-4993-88b6-a6d36024a4e4
caps.latest.revision: 42
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 817de3b9232a755d94fe2790a0ab2e08a835c9dc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37163509"
---
# <a name="content-types-data-mining"></a>內容類型 (資料採礦)
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，您可以同時定義採礦結構中資料行的實體資料類型，以及用於模型內之資料行的邏輯內容類型。  
  
 *「資料類型」* 會決定當您建立採礦模型時，演算法要如何處理這些資料行中的資料。 定義資料行的資料類型會提供資訊給演算法，這是有關資料行中的資料類型及如何處理資料的資訊。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的每一個資料類型都會支援一個或多個適用於資料採礦的內容類型。  
  
 *「內容類型」* 會描述資料行所包含之內容的行為。 例如，若資料行中的內容以特定間隔重複 (例如每星期幾)，您可以指定資料行的內容類型為循環。  
  
 有些演算法需要特定資料類型和內容類型才能正確運作。 例如，Microsoft 貝氏機率分類演算法無法使用連續資料行做為輸入，也無法預測連續值。 某些內容類型 (如 Key Sequence) 只會由特定的演算法所使用。 如需演算法清單和各演算法支援的內容類型，請參閱[資料採礦演算法 &#40;Analysis Services-資料採礦 &#41;](data-mining-algorithms-analysis-services-data-mining.md)。  
  
 下列清單描述資料採礦中使用的內容類型，並識別支援每一種類型的資料類型。  
  
## <a name="discrete"></a>Discrete  
 *Discrete* 代表資料行包含有限數量的值，且值之間沒有延續。 例如，性別資料行是一個典型的離散屬性資料行，因為其資料代表特定數量的類別。  
  
 離散屬性資料行中的值不代表順序，即使值為數值。 此外，即使用於離散資料行的值為數值，也無法計算小數值。 電話區碼是數字分隔資料的理想範例。  
  
 `Discrete`內容類型受到所有資料採礦資料類型。  
  
## <a name="continuous"></a>Continuous  
 *Continuous* 表示此資料行包含的值代表小數位數允許過渡值的數值資料。 與代表有限可計算資料的離散資料行不同，連續資料行代表可擴充的度量，其資料可能包含無限個小數值。 溫度資料行就是連續屬性資料行的一個範例。  
  
 當資料行包含連續數值資料，而且您知道應該要如何散發資料時，您可以指定預期的值分佈來提升分析的精確度。 您會在採礦結構的層級上指定資料行散發。 因此，此設定會套用到根據此結構的所有模型上。如需詳細資訊，請參閱[資料行散發 &#40;資料採礦&#41;](column-distributions-data-mining.md)。  
  
 `Continuous`內容類型受到下列資料類型： `Date`， `Double`，和`Long`。  
  
## <a name="discretized"></a>Discretized  
 *「離散化」* (Discretization) 是將連續資料集的值放入值區內的程序，以產生有限數目的可能值。 您只能離散化數值資料。  
  
 因此， *「離散化」* (Discretized) 內容類型表示此資料行包含的值代表從連續資料行衍生之值的群組或值區。 貯體會被當成已排序的離散值來處理。  
  
 您可以手動離散化資料，以確保您能取得所要的值區，或者可以使用在 SQL Server Analysis Services 中提供的離散化方法。 某些演算法會自動執行離散化。 如需詳細資訊，請參閱 [變更採礦模型中的資料行分隔](change-the-discretization-of-a-column-in-a-mining-model.md)。  
  
 `Discretized` 內容類型受到下列資料類型的支援：`Date`、`Double`、`Long` 和 `Text`。  
  
## <a name="key"></a>索引鍵  
 *key* 內容類型表示資料行會唯一識別資料列。 在案例資料表中，索引鍵資料行通常是數值的或文字的識別碼。 您將內容類型設定為`key`表示資料行不應該使用的分析，只能用於追蹤記錄。  
  
 巢狀資料表也具有索引鍵，但巢狀資料表索引鍵的用法稍有不同。 您將內容類型設定為`key`中巢狀資料表資料行是否為您想要分析的屬性。 每個案例的巢狀資料表索引鍵值都必須是唯一的，但在整個案例集合中可能會有重複的值。  
  
 例如，如果要分析客戶購買的產品，則可以將內容類型設定為案例資料表中 **CustomerID** 資料行的索引鍵，然後再次將內容類型設定為巢狀資料表中 **PurchasedProducts** 資料行的索引鍵。  
  
> [!NOTE]  
>  只有在從已定義為 Analysis Services 資料來源檢視的外部資料來源使用資料時，才可以使用巢狀資料表。  
  
 此內容類型受到下列資料類型： `Date`， `Double`， `Long`，和`Text`。  
  
## <a name="key-sequence"></a>Key Sequence  
 *key sequence* 內容類型只能用於時序群集模型。 將內容類型設定為 `key sequence` 時，代表資料行包含代表事件序列的值。 其值已排序，但不必為等距。  
  
 此內容類型受到下列資料類型： `Double`， `Long`， `Text`，和`Date`。  
  
## <a name="key-time"></a>Key Time  
 *key time* 內容類型只能用於時間序列模型。 將內容類型設定為 `key time` 時，代表值已排序且代表時段。  
  
 這個內容類型受到下列資料類型所支援：`Double`、`Long` 和 `Date`。  
  
## <a name="table"></a>Table  
 *table* 內容類型表示資料行包含另一個資料表，資料表內有一個或多個資料行及一個或多個資料列。 對於案例資料表中的任何特定資料列，這個資料行也可以包含多個全與父案例記錄相關的值。 例如，如果主要案例資料表包含客戶清單，則您可以擁有數個包含巢狀資料表的資料行，例如 **ProductsPurchased** 資料行 (其中巢狀資料表會列出此客戶過去購買的產品) 及 **Hobbies** 資料行 (列出客戶興趣)。  
  
 此資料行的資料類型一定是 `Table`。  
  
## <a name="cyclical"></a>Cyclical  
 *cyclical* 內容類型表示資料行包含了代表循環之已排序集合的值。 例如，有編號的星期幾就是一個循環已排序集合，因為第 7 天後面就是第 1 天。  
  
 在內容類型方面，循環資料行會被視為已排序且分隔。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中的所有資料採礦資料類型，都支援此內容類型。 不過，大部分的演算法將循環值視為離散值，因此不會執行特殊處理。  
  
## <a name="ordered"></a>Ordered  
 *Ordered* 內容類型也表示包含了定義順序或次序之值的資料行。 但是，在這個內容類型中，用於排序的值不表示該集合中各值之間的距離或大小關聯性。 例如，若已排序屬性資料行包含有關技能層級的資訊，按照 1 到 5 的次序排序，則技能層級之間的距離沒有任何隱含資訊；技能層級 5 不一定比技能層級 1 好 5 倍。  
  
 在內容類型方面，已排序屬性資料行會被視為分隔。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中的所有資料採礦資料類型，都支援此內容類型。 不過，大部分的演算法將已排序的值視為離散值，因此不會執行特殊處理。  
  
## <a name="classified"></a>Classified  
 除了前述常用於所有模型的內容類型之外，您可以使用分類資料行來定義某些資料類型的內容類型。 如需分類資料行的詳細資訊，請參閱[分類資料行 &#40;資料採礦&#41;](classified-columns-data-mining.md)。  
  
## <a name="see-also"></a>另請參閱  
 [內容類型&#40;DMX&#41;](/sql/dmx/content-types-dmx)   
 [資料型別&#40;資料採礦&#41;](data-types-data-mining.md)   
 [資料型別&#40;DMX&#41;](/sql/dmx/data-types-dmx)   
 [變更採礦結構的屬性](change-the-properties-of-a-mining-structure.md)   
 [採礦結構資料行](mining-structure-columns.md)  
  
  
