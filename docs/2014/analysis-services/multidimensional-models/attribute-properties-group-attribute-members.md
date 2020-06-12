---
title: 群組屬性成員（離散化） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- NameColumn property
- discretization [Analysis Services]
- member groups [Analysis Services]
- grouping members
- DiscretizationNumber property
- sort orders [Analysis Services]
- DiscretizationMethod property
- adding members to member group
- number of member groups
- members [Analysis Services], groups
- names [Analysis Services], member groups
ms.assetid: 5cf2f407-accc-4baf-b54f-7703af338325
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7e2c52ec93b46418b82b681fbacc1d31338a0d88
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544780"
---
# <a name="group-attribute-members-discretization"></a>群組屬性成員 (分隔)
  成員群組是系統產生之連續維度成員的集合。 在中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，屬性的成員可以透過稱為「離散化」的進程，分組到多個成員群組中。 階層中的層級包含成員群組或成員，但不會同時包含兩者。 商務使用者瀏覽含有成員群組的層級時，他們會看到成員群組的名稱和資料格值。 由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 產生以支援成員群組的成員稱為群組成員，看起來就像一般成員。  
  
 屬性 (Attribute) 上的 `DiscretizationMethod` 屬性 (Property)，控制如何將成員群組。  
  
|`DiscretizationMethod` 設定|Description|  
|--------------------------------------|-----------------|  
|`None`|顯示成員。|  
|`Automatic`|請選取最適合代表資料的方法：`EqualAreas` 方法或 `Clusters` 方法。|  
|`EqualAreas`|嘗試將屬性中的成員分成包含相同成員數目的群組。|  
|`Clusters`|取樣培訓資料、初始化為一些隨機點，然後執行最大期望 (EM) 群集演算法的數次反覆運算，嘗試將屬性中的成員分成群組。<br /><br /> 這個方法適用於任何分佈曲線，所以十分有用，但是需要較多的處理時間。|  
  
 屬性 (Attribute) 上的 `DiscretizationNumber` 屬性 (Property)，指定要顯示的群組數目。 如果屬性是設定為預設值 0，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會取樣或讀取資料 (視 `DiscretizationMethod` 屬性的設定而定)，以決定群組的數目。  
  
 成員群組中之成員的排序順序是由屬性 (Attribute) 的 `OrderBy` 屬性 (Property) 所控制。 會根據這個排序順序，將成員群組中的成員連續排序。  
  
 成員群組一般是用來從具有少數成員的層級向下鑽研至具有許多成員的層級。 若要讓使用者在層級間進行向下鑽研，請將含有許多成員之層級屬性 (Attribute) 上的 `DiscretizationMethod` 屬性 (Property)，從 `None` 變更為上表所描述的其中一個分隔方法。 例如，Client 維度包含擁有 500,000 個成員的 Client Name 屬性階層。 您可以將此屬性 (Attribute) 重新命名為 Client Groups，並將 `DiscretizationMethod` 屬性 (Property) 設定為 `Automatic`，以顯示屬性 (Attribute) 階層成員層級上的成員群組。  
  
 若要向下鑽研至每個群組中的個別客戶，則您可以建立繫結到相同資料表資料行的另一個 Client Name 屬性階層。 然後，依據兩個屬性建立新的使用者階層。 最上層是以 Client Groups 屬性為基礎，而下層則是以 Client Name 屬性為基礎。 兩個屬性 (Attribute) 上的 `IsAggregatable` 屬性 (Property) 會是 `True`。 然後，使用者可以展開階層上的 (全部) 層級以檢視群組成員，並展開群組成員以檢視階層的分葉成員。 若要隱藏群組或客戶層級，您可以將對應屬性 (Attribute) 上的 `AttributeHierarchyVisible` 屬性 (Property) 設定為 `False`。  
  
## <a name="naming-template"></a>命名範本  
 建立成員群組時，會自動產生成員群組名稱。 除非您指定命名範本，否則會使用預設命名範本。 而在屬性 (Attribute) 之 `Format` 屬性 (Property) 的 `NameColumn` 選項中指定命名範本，即可變更這個命名方法。 也可以針對用於屬性 (Attribute) 之 `Translations` 屬性 (Property) 之資料行繫結的 `NameColumn` 集合中所指定的每個語言，來重新定義不同的命名範本。  
  
 `Format` 設定會使用下列字串運算式，來定義命名範本：  
  
 `<Naming template> ::= <First definition> [;<Intermediate definition>;<Last definition>]`  
  
 `<First definition> ::= <Name expression>`  
  
 `<Intermediate definition> ::= <Name expression>`  
  
 `<Last definition> ::= <Name expression>`  
  
 `<First definition>` 參數只適用於分隔方法所產生的第一個，或唯一的一個成員群組。 如果未提供選擇性參數 `<Intermediate definition>` 和 `<Last definition>` ，則會將 `<First definition>` 參數用於針對該屬性所產生的所有量值群組。  
  
 `<Last definition>` 參數只適用於分隔方法所產生的最後一個成員群組。  
  
 `<Intermediate bucket name>` 參數適用於分隔方法所產生之第一個或最後一個成員群組以外的每一個成員群組。 如果只產生兩個或更少的成員群組，就會忽略此參數。  
  
 `<Bucket name>` 參數是一個字串運算式，其中可以納入一組變數，在其成員群組名稱中代表成員或成員群組資訊：  
  
|變數|描述|  
|--------------|-----------------|  
|%{First bucket member}|要包含在目前成員群組中之第一個成員的成員名稱。|  
|%{Last bucket member}|要包含在目前成員群組中之最後一個成員的成員名稱。|  
|%{Previous bucket last member}|指派至前一個成員群組之最後一個成員的成員名稱。|  
|%{Next bucket first member}|指派至下一個成員群組之第一個成員的成員名稱。|  
|%{Bucket Min}|要指派至目前成員群組之成員的最小值。|  
|%{Bucket Max}|要指派至目前成員群組之成員的最大值。|  
|%{Previous Bucket Max}|要指派至前一個成員群組之成員的最大值。|  
|%{Next Bucket Min}|要指派至下一個成員群組之成員的最小值。|  
  
 預設命名範本是 `"%{First bucket member} - %{Last bucket member}"`，以提供與舊版 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的相容性。  
  
> [!NOTE]  
>  若要在命名範本中將分號 (;) 併入成常值字元，請在它的前面加上百分比 (%) 字元。  
  
### <a name="example"></a>範例  
 下列字串運算式可用來分類 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 範例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中之 Customer 維度的 Yearly Income 屬性，而 Yearly Income 屬性使用成員群組：  
  
 "Less than %{Next Bucket Min};Between %{First bucket member} and %{Last bucket member};Greater than %{Previous Bucket Max}"  
  
## <a name="adding-new-members-to-existing-member-groups"></a>將新成員加入至現有的成員群組  
 如果將新成員加入至維度，就會以新成員的值比較目前的成員群組配置，將新成員指派至適當的成員群組。  
  
 如果成員插入至上一個成員群組的最後一個成員以及下一個成員群組的第一個成員之間，新的成員就會變成上一個成員群組的最後一個成員。  
  
## <a name="updating-a-dimension-with-discretized-attributes"></a>更新具有分隔屬性的維度  
 當您處理維度時，只會使用完整更新 (ProcessFull) 重新分隔分隔屬性。 若要重新分隔屬性，您必須執行維度的完整更新。 如果分隔屬性的維度資料表已更新，而且您是使用累加式更新 (ProcessAdd) 來處理維度，將不會重新分隔分隔屬性。 新值區的名稱和子系會保持相同。 如需處理維度的詳細資訊，請參閱 [處理 Analysis Services 物件](processing-analysis-services-objects.md)。  
  
## <a name="usage-limitations"></a>使用方式的限制  
  
-   您無法在階層的最頂端或最底端層級建立成員群組。 然而，如果需要這樣做，您可以用這樣的方式新增一個層級，這樣您要在其中建立成員群組的層級就不再是頂端或底端層級。 您可以將加入之層級的 `Visible` 屬性設定為 `False`，來隱藏加入的層級。  
  
-   您不能在階層的兩個連續層級中建立成員群組。  
  
-   使用 ROLAP 儲存模式的維度，並不支援成員群組。  
  
-   如果更新包含成員群組之維度的維度資料表，然後又完全處理維度，就會產生新的成員群組集。 新成員群組的名稱與子系，可能會與舊的成員群組不同。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
