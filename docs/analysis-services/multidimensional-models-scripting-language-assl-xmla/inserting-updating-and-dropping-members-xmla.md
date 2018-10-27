---
title: 插入、 更新和卸除成員 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3a409e21e925b3912aee5ec751747f61bce05276
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147323"
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>插入、更新和卸除成員 (XMLA)
  您可以使用[插入](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)，[更新](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)，並[卸除](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)命令在 XML for Analysis (XMLA) 分別插入、 更新或刪除成員，從可寫入的維度。 如需有關可寫入維度的詳細資訊，請參閱[Write-Enabled 維度](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)。  
  
## <a name="inserting-new-members"></a>插入新成員  
 **插入**命令會將新成員插入可寫入維度中的指定屬性。  
  
 建構之前**插入**命令時，您應該有下列可用於插入新成員的資訊：  
  
-   要在其中插入新成員的維度。  
  
-   要在其中插入新成員的維度屬性。  
  
-   新成員的名稱，包括任何適用的名稱翻譯。  
  
-   新成員的索引鍵。 如果屬性使用複合索引鍵，索引鍵可能需要多個值。  
  
-   並未像其他的屬性已實作在維度中，但適用的任何屬性值。 這樣的屬性包括一元運算、翻譯、自訂積存、自訂積存屬性以及略過的層級。  
  
 **插入**命令會將只有兩個屬性：  
  
-   [物件](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)屬性，其中包含成員之維度中要插入的物件參考。 物件參考包含資料庫識別碼、Cube 識別碼以及維度的維度識別碼。  
  
-   [屬性](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attributes-element-xmla)屬性，其中包含一或多個[屬性](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attribute-element-xmla)識別成員的屬性中要插入的項目。 每個**屬性**項目將屬性識別與提供名稱、 值、 翻譯、 一元運算子、 自訂積存、 自訂積存屬性以及略過單一識別屬性要加入成員的層級。  
  
    > [!NOTE]  
    >  所有的屬性，如**屬性**必須包含項目。 否則，系統可能會發生錯誤。  
  
## <a name="updating-existing-members"></a>更新現有的成員  
 **更新**命令會更新指定的屬性，以與其他屬性，在可寫入的維度中的其他成員的關聯性中的現有成員。 **更新**命令可以移至階層中的其他層級的成員包含的維度，而且可用來重新建構的父子式階層的父屬性所定義。  
  
 建構之前**更新**命令時，您應該要更新之成員可用的下列資訊：  
  
-   要在其中更新現有成員的維度。  
  
-   要在其中更新現有成員的維度屬性。  
  
-   現有成員的索引鍵。 如果屬性使用複合索引鍵，索引鍵可能需要多個值。  
  
-   並未像其他的屬性已實作在維度中，但適用的任何屬性值。 這樣的屬性包括一元運算、翻譯、自訂積存、自訂積存屬性以及略過的層級。  
  
 **更新**命令會將只有三個必要的屬性：  
  
-   **物件**屬性，其中包含成員之維度中要更新的物件參考。 物件參考包含資料庫識別碼、Cube 識別碼以及維度的維度識別碼。  
  
-   **屬性**屬性，其中包含一或多個**屬性**元素，以識別成員的屬性在其中更新。 **屬性**項目將屬性識別與提供名稱、 值、 翻譯、 一元運算子、 自訂積存、 自訂積存屬性以及略過更新為識別屬性的單一成員的層級。  
  
    > [!NOTE]  
    >  所有的屬性，如**屬性**必須包含項目。 否則，系統可能會發生錯誤。  
  
-   [何處](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/where-element-xmla)屬性，其中包含一或多個**屬性**限制成員要更新的屬性的項目。 **何處**屬性，請務必限制**更新**命令成員的特定執行個體。 如果**其中**屬性未指定，會更新指定成員的所有執行個體。 例如，您要將三個客戶的城市名稱從 Redmond 變更為 Bellevue。 若要變更城市名稱，您必須提供**其中**屬性可識別客戶中的三個成員屬性應該變更 City 屬性中的成員。 如果您未提供這**何處**屬性，其城市名稱目前為 Redmond 的每個客戶會有縣 （市） 名稱之後變成 bellevue**更新**命令會執行。  
  
    > [!NOTE]  
    >  新的成員，除了**更新**命令只能更新未包含在屬性的屬性索引鍵值**其中**子句。 例如，更新客戶時無法更新城市名稱，否則會為所有客戶變更城市名稱。  
  
### <a name="updating-members-in-parent-attributes"></a>更新父屬性中的成員  
 為了支援父屬性**更新**命令有選擇性[MoveWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/movewithdescendants-element-xmla)MovewithDescedants 屬性。 設定**MoveWithDescendants**屬性設為 true 表示父成員之下階應該也能移動與父成員的識別碼，該父成員變更時。 如果這個值是設定為 false，移動父成員會造成該父成員的直接下階升級為父成員先前所在的層級。  
  
 當更新父屬性中的成員**更新**命令不能更新其他屬性中的成員。  
  
## <a name="dropping-existing-members"></a>卸除現有的成員  
 建構之前**卸除**命令時，您應該要卸除之成員可用的下列資訊：  
  
-   要在其中卸除現有成員的維度。  
  
-   要在其中卸除現有成員的維度屬性。  
  
-   要卸除之現有成員的索引鍵。 如果屬性使用複合索引鍵，索引鍵可能需要多個值。  
  
 **卸除**命令會將只有兩個必要的屬性：  
  
-   **物件**屬性，其中包含成員之維度中卸除的物件參考。 物件參考包含資料庫識別碼、Cube 識別碼以及維度的維度識別碼。  
  
-   **何處**屬性，其中包含一或多個**屬性**限制成員的屬性中要刪除的項目。 **何處**屬性，請務必限制**卸除**命令成員的特定執行個體。 如果**其中**命令未指定，會卸除指定的成員的所有執行個體。 例如，您要從 Redmond 卸除三個客戶。 若要卸除這些客戶，您必須提供**其中**屬性以識別 Customer 屬性中移除的三個成員和其三個客戶的要移除的 City 屬性之 Redmond 成員。 如果**何處**屬性只指定 City 屬性之 Redmond 成員時，會卸除與 Redmond 關聯的每個客戶的**卸除**命令。 如果**何處**屬性只在 Customer 屬性中指定的三個成員，就會完全由刪除三個客戶**卸除**命令。  
  
    > [!NOTE]  
    >  **屬性**中包含的項目**卸除**命令必須只包含**AttributeName**並**金鑰**屬性。 否則，系統可能會發生錯誤。  
  
### <a name="dropping-members-in-parent-attributes"></a>卸除父屬性中的成員  
 設定[DeleteWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/deletewithdescendants-element-xmla)屬性會指出也應該隨父成員刪除的父成員下階。 如果這個值是設定為 false，則會改將父成員的直接下階升級為父成員先前所在的層級。  
  
> [!IMPORTANT]  
>  使用者只要擁有父成員的刪除權限，即可同時刪除父成員及其子階。 使用者不需要子階的刪除權限。  
  
## <a name="see-also"></a>另請參閱  
 [卸除項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)   
 [插入項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)   
 [更新項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [定義和識別物件&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)   
 [在 Analysis Services 中使用 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
