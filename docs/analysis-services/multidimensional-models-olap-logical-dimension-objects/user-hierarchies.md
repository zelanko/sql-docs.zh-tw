---
title: "使用者階層 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- members [Analysis Services], hierarchies
- dimensions [Analysis Services], hierarchies
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], attribute
- attributes [Analysis Services], hierarchies
- parent-child hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
- ragged hierarchies [Analysis Services]
- balanced hierarchies [Analysis Services]
- hierarchies [Analysis Services]
- OLAP objects [Analysis Services], hierarchies
- multilevel hierarchies [Analysis Services]
- unbalanced hierarchies [Analysis Services]
ms.assetid: 9394e9a3-2242-4f0e-85e0-25d499d2d3b6
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a62551b69a8d14dbb860976d2c8b70b10b92186a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="user-hierarchies"></a>使用者階層
  使用者定義階層是使用者定義的屬性中所使用的階層[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]維度的成員組織成階層式結構，並提供 cube 中的導覽路徑。 例如，下表定義時間維度的維度資料表， 此維度資料表支援三個屬性，名為年份、季度和月份。  
  
|Year|Quarter|Month|  
|----------|-------------|-----------|  
|1999|第一季|一月|  
|1999|第一季|二月|  
|1999|第一季|三月|  
|1999|第二季|四月|  
|1999|第二季|五月|  
|1999|第二季|六月|  
|1999|第三季|七月|  
|1999|第三季|八月|  
|1999|第三季|九月|  
|1999|第四季|Oct|  
|1999|第四季|十一月|  
|1999|第四季|Dec|  
  
 使用年份、季度和月份屬性，即可在時間維度中建構名為「日曆」的使用者自訂階層。 日曆維度 (一個一般維度) 的層級和成員之間的關聯性如下圖所示：  
  
 ![針對時間維度的層級和成員階層](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/media/as-levelconcepts.gif "時間維度的階層層級和成員")  
  
> [!NOTE]  
>  預設兩層級屬性階層之外的任何階層都稱為使用者自訂階層。 如需有關屬性階層的詳細資訊，請參閱[屬性和屬性階層](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)。  
  
## <a name="member-structures"></a>成員結構  
 除了父子式階層以外，成員在階層內的位置是由階層定義裡之屬性的順序控制。 此階層定義中的每一個屬性都會在階層中組成一個層級； 層級內之成員的位置，是由用來建立層級之屬性的順序決定。 使用者自訂階層的成員結構依成員間互相關聯的方式，可以具有四種基本形式之一。  
  
### <a name="balanced-hierarchies"></a>對稱的階層  
 在對稱的階層中，階層的所有分支均下降至同一層級，而且每一個成員的邏輯父系就是直接在該成員上面的層級。 在 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 範例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中，產品維度的產品類別目錄階層即為對稱階層的良好範例。 產品名稱層級中的每個成員，在子類別目錄層級裡有一個父成員，而後者則在類別目錄層級內有一個父成員。 此外，階層中的每個分支都可以有產品名稱層級中的分葉成員。  
  
### <a name="unbalanced-hierarchies"></a>不對稱的階層  
 在不對稱的階層中，階層的分支下降至不同的層級。 父子式階層即為不對稱的階層。 例如，[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 範例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中的組織維度會包含每位員工的成員。 CEO 是階層中的頂部成員，而部門經理和執行秘書則是直接在 CEO 底下。 部門經理有從屬成員，但是執行秘書沒有。  
  
 一般使用者可能根本無法區分不對稱的和不完全的階層。 然而，您可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中使用不同的技術和屬性，以支援這兩種類型的階層。 如需詳細資訊，請參閱[不完全階層](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md)，和[父子式階層中的屬性](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)。  
  
### <a name="ragged-hierarchies"></a>不完全階層  
 在不完全的階層中，至少一個成員的邏輯父成員不在成員的上一層級內。 這樣將會使階層的分支下降至不同的層級。 例如，在定義了大陸、國家 (地區) 和縣 (市) 層級的地理位置維度中，依照該順序，Europe 成員會在階層的最上層顯示、France 成員在中間層顯示，而 Paris 成員則在最下層顯示。 France 比 Europe 更為具體，而 Paris 又比 France 更為具體。 對於這個一般階層，會進行下列變更：  
  
-   將 Vatican City 成員加入國家 (地區) 層級中。  
  
-   成員會加入縣 (市) 層級，並與國家 (地區) 層級中的 Vatican City 成員產生關聯。  
  
-   在國家 (地區) 和縣 (市) 層級之間加入名為省份的層級。  
  
 省份層級會使用與國家 (地區) 層級中之其他成員相關聯的成員進行擴展，而縣 (市) 層級中的成員會與省份層級中之對應的成員相關聯。 但是，由於國家 (地區) 層級中的 Vatican City 成員在省份層級裡沒有關聯的成員，因此必須直接從縣 (市) 層級，將成員與國家 (地區) 層級裡的 Vatican City 成員相關聯。 因為這些變更，所以維度的階層會變成不完全。 Vatican City 縣 (市) 的父系是 Vatican City 國家 (地區)，這並不會在國家 (地區) 層級中 Vatican City 成員的直接上層層級裡。 如需詳細資訊，請參閱 [不完全階層](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md)。  
  
### <a name="parent-child-hierarchies"></a>父子式階層  
 維度的父子式階層是使用一個特殊屬性 (稱為父屬性) 定義，以決定各成員如何互相關聯。 父屬性描述維度主資料表內的「自我參考關聯性」或「自我聯結」。 父子式階層是由單一父屬性所建構的。 因為階層中的層級是從與父屬性相關之成員間的父子式關聯性衍生而來，所以只會將一個層級指派給父子式階層。 父子式階層的維度結構描述，相依於維度主資料表上所顯示的自我參考關聯性。 例如下, 圖說明**DimOrganization**中的維度主資料表[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]範例資料庫。  
  
 ![DimOrganization 資料表中的自我參考聯結](../../analysis-services/multidimensional-models/media/dimorganization.gif "DimOrganization 資料表中的自我參考聯結")  
  
 在這份維度資料表中， **ParentOrganizationKey** 資料行與 **OrganizationKey** 主索引鍵資料行具有外部索引鍵關聯性。 換句話說，此資料表中的每一個記錄均可透過父子式關聯性與資料表中的另一個記錄相關。 這種自我聯結通常用來呈現組織實體資料 (例如，部門內之員工的管理結構)。  
  
 您建立父子式階層時，兩個屬性所代表的資料行，必須有相同的資料類型。 這兩個屬性也必須在同一個資料表中。 依預設，如果成員的父索引鍵等於其本身的索引鍵、為 Null、0 (零)，或在成員索引鍵之資料行中沒有的值，成員就會被假設為頂部層級的成員 ((全部) 層級除外)。  
  
 各階層分支中的父子式階層深度會不同。 換句話說，會將父子式階層視為不對稱的階層。  
  
 使用者自訂階層中的層級數目會決定使用者可看到的層級數目，而父子式階層則與使用者自訂階層不同，是由屬性階層的單一層級所定義，而這個單一層級中的值會產生使用者可看到的多個層級。 顯示之層級的數目，會視儲存成員索引鍵和父索引鍵之維度資料表資料行的內容而定。 維度資料表中的資料變更時，層級的數目可能會變更。 如需詳細資訊，請參閱[父子式維度](../../analysis-services/multidimensional-models/parent-child-dimension.md)，和[父子式階層中的屬性](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立使用者定義階層](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)   
 [使用者階層屬性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [維度屬性 (Attribute) 屬性 (Property) 參考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  

