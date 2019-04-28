---
title: 插入、 更新和卸除成員 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- inserting dimension members
- XML for Analysis, members
- removing dimension members
- dropping dimension members
- write-enabled dimensions [Analysis Services]
- XMLA, members
- deleting dimension members
- dimensions [Analysis Services], XML for Analysis
ms.assetid: bba922b5-8b88-4051-9506-ff055248182a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 98da3e0f7a9b61b178372d9b24b8b595ab6b6626
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727162"
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>插入、更新和卸除成員 (XMLA)
  您可以使用[插入](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)，[更新](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)，並[卸除](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)命令在 XML for Analysis (XMLA) 分別插入、 更新或刪除成員，從可寫入的維度。 如需有關可寫入維度的詳細資訊，請參閱[Write-Enabled 維度](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)。  
  
## <a name="inserting-new-members"></a>插入新成員  
 `Insert` 命令會將新的成員插入可寫入維度中的特定屬性。  
  
 在建構 `Insert` 命令之前，您應該有下列可用於插入新成員的資訊：  
  
-   要在其中插入新成員的維度。  
  
-   要在其中插入新成員的維度屬性。  
  
-   新成員的名稱，包括任何適用的名稱翻譯。  
  
-   新成員的索引鍵。 如果屬性使用複合索引鍵，索引鍵可能需要多個值。  
  
-   並未像其他的屬性已實作在維度中，但適用的任何屬性值。 這樣的屬性包括一元運算、翻譯、自訂積存、自訂積存屬性以及略過的層級。  
  
 `Insert` 命令只使用兩個屬性：  
  
-   [物件](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)屬性，其中包含成員之維度中要插入的物件參考。 物件參考包含資料庫識別碼、Cube 識別碼以及維度的維度識別碼。  
  
-   [屬性](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attributes-element-xmla)屬性，其中包含一或多個[屬性](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attribute-element-xmla)識別成員的屬性中要插入的項目。 每個 `Attribute` 元素可識別屬性，並為要加入識別屬性的單一成員提供名稱、值、翻譯、一元運算子、自訂積存、自訂積存屬性以及略過的層級。  
  
    > [!NOTE]  
    >  `Attribute` 元素的所有屬性都必須包含在內。 否則，系統可能會發生錯誤。  
  
## <a name="updating-existing-members"></a>更新現有的成員  
 `Update` 命令會根據與其他屬性中其他成員的關係，在可寫入的維度之指定屬性中更新現有的成員。 `Update` 命令可以將成員移到維度所含的階層中之其他層級，而且可用以重新設定父屬性所定義的父子式階層之結構。  
  
 在建構 `Update` 命令之前，您應該有下列可用於更新成員的資訊：  
  
-   要在其中更新現有成員的維度。  
  
-   要在其中更新現有成員的維度屬性。  
  
-   現有成員的索引鍵。 如果屬性使用複合索引鍵，索引鍵可能需要多個值。  
  
-   並未像其他的屬性已實作在維度中，但適用的任何屬性值。 這樣的屬性包括一元運算、翻譯、自訂積存、自訂積存屬性以及略過的層級。  
  
 `Update` 命令只使用三個必要的屬性：  
  
-   `Object` 屬性，包含要在其中更新成員之維度的物件參考。 物件參考包含資料庫識別碼、Cube 識別碼以及維度的維度識別碼。  
  
-   `Attributes` 屬性，包含一或多個 `Attribute` 元素，以識別要在其中更新成員的屬性。 `Attribute` 元素可識別屬性，並為識別屬性要更新的單一成員提供名稱、值、翻譯、一元運算子、自訂積存、自訂積存屬性以及略過的層級。  
  
    > [!NOTE]  
    >  `Attribute` 元素的所有屬性都必須包含在內。 否則，系統可能會發生錯誤。  
  
-   [何處](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/where-element-xmla)屬性，其中包含一或多個`Attribute`限制成員要更新的屬性的項目。 `Where` 屬性對於將 `Update` 命令限制在成員的特定執行個體來說十分重要。 如果`Where`屬性未指定，會更新指定成員的所有執行個體。 例如，您要將三個客戶的城市名稱從 Redmond 變更為 Bellevue。 若要變更城市名稱，您必須提供 `Where` 屬性以識別 Customer 屬性中應該變更的三個 City 屬性成員。 如果您沒有提供這個 `Where` 屬性，則城市名稱目前為 Redmond 的每個客戶，在執行 `Update` 命令之後，其城市名稱都將變成 Bellevue。  
  
    > [!NOTE]  
    >  除了新成員之外，`Update` 命令只能為不包含在 `Where` 子句中的屬性更新屬性索引鍵值。 例如，更新客戶時無法更新城市名稱，否則會為所有客戶變更城市名稱。  
  
### <a name="updating-members-in-parent-attributes"></a>更新父屬性中的成員  
 為了支援父屬性`Update`命令有選擇性[MoveWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/movewithdescendants-element-xmla)MovewithDescedants 屬性。 將 `MoveWithDescendants` 屬性設定為 true，以指定在該父成員識別碼變更時，父成員的下階也應該隨父成員一起移動。 如果這個值是設定為 false，移動父成員會造成該父成員的直接下階升級為父成員先前所在的層級。  
  
 在父屬性中更新成員時，`Update` 命令無法更新其他屬性中的成員。  
  
## <a name="dropping-existing-members"></a>卸除現有的成員  
 在建構 `Drop` 命令之前，您應該有下列可用於卸除成員的資訊：  
  
-   要在其中卸除現有成員的維度。  
  
-   要在其中卸除現有成員的維度屬性。  
  
-   要卸除之現有成員的索引鍵。 如果屬性使用複合索引鍵，索引鍵可能需要多個值。  
  
 `Drop` 命令只使用兩個必要的屬性：  
  
-   `Object` 屬性，包含要在其中卸除成員之維度的物件參考。 物件參考包含資料庫識別碼、Cube 識別碼以及維度的維度識別碼。  
  
-   `Where` 屬性包含一或多個 `Attribute` 元素，會限制要在其中刪除成員的屬性。 `Where` 屬性對於將 `Drop` 命令限制在成員的特定執行個體來說十分重要。 如果未指定 `Where`命令，指定成員的所有執行個體都會卸除。 例如，您要從 Redmond 卸除三個客戶。 若要卸除這些客戶，您必須提供 `Where` 屬性以識別 Customer 屬性中要移除的三個成員，以及要從 City 屬性之 Redmond 成員中移除的三個客戶。 如果 `Where` 屬性只指定 City 屬性的 Redmond 成員，則 `Drop` 命令會卸除與 Redmond 關聯的每個客戶。 如果 `Where` 屬性只在 Customer 屬性中指定三個成員，則 `Drop` 命令會完全刪除這三個客戶。  
  
    > [!NOTE]  
    >  包括在 `Attribute` 命令中的 `Drop` 元素必須只包含 `AttributeName` 與 `Keys` 屬性。 否則，系統可能會發生錯誤。  
  
### <a name="dropping-members-in-parent-attributes"></a>卸除父屬性中的成員  
 設定[DeleteWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/deletewithdescendants-element-xmla)屬性會指出也應該隨父成員刪除的父成員下階。 如果這個值是設定為 false，則會改將父成員的直接下階升級為父成員先前所在的層級。  
  
> [!IMPORTANT]  
>  使用者只要擁有父成員的刪除權限，即可同時刪除父成員及其子階。 使用者不需要子階的刪除權限。  
  
## <a name="see-also"></a>另請參閱  
 [卸除項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)   
 [插入項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)   
 [更新項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [定義和識別物件&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)   
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
