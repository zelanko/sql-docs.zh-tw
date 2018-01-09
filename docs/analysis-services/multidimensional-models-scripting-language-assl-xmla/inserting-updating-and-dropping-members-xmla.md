---
title: "插入、 更新和卸除成員 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
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
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 17c8d0a3fddeb0cfd9d8a6ef69eac11bc9b2c34a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>插入、更新和卸除成員 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]您可以使用[插入](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[更新](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)，和[卸除](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)命令在 XML for Analysis (XMLA) 分別插入、 更新或刪除從可寫入維度的成員。 如需啟用寫入的維度的詳細資訊，請參閱[Write-Enabled 維度](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)。  
  
## <a name="inserting-new-members"></a>插入新成員  
 **插入**命令會將新成員插入可寫入維度中的指定屬性。  
  
 建構前**插入**命令時，您應該有可用於插入新成員的下列資訊：  
  
-   要在其中插入新成員的維度。  
  
-   要在其中插入新成員的維度屬性。  
  
-   新成員的名稱，包括任何適用的名稱翻譯。  
  
-   新成員的索引鍵。 如果屬性使用複合索引鍵，索引鍵可能需要多個值。  
  
-   並未像其他的屬性已實作在維度中，但適用的任何屬性值。 這樣的屬性包括一元運算、翻譯、自訂積存、自訂積存屬性以及略過的層級。  
  
 **插入**命令使用只有兩個屬性：  
  
-   [物件](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)屬性，其中包含的維度成員要插入的物件參考。 物件參考包含資料庫識別碼、Cube 識別碼以及維度的維度識別碼。  
  
-   [屬性](../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)屬性，其中包含一或多個[屬性](../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)元素，以識別成員要插入的屬性。 每個**屬性**元素可識別屬性並提供名稱、 值、 翻譯、 一元運算子、 自訂積存、 自訂積存屬性以及略過加入識別屬性的單一成員的層級。  
  
    > [!NOTE]  
    >  所有屬性**屬性**必須包含項目。 否則，系統可能會發生錯誤。  
  
## <a name="updating-existing-members"></a>更新現有的成員  
 **更新**命令會更新指定的屬性，根據與其他成員可寫入維度中的其他屬性中的關聯性中的現有成員。 **更新**命令可以移動階層中的其他層級的成員包含的維度，而且可用來重建父屬性所定義的父子式階層。  
  
 建構前**更新**命令時，您應該有可用於更新成員的下列資訊：  
  
-   要在其中更新現有成員的維度。  
  
-   要在其中更新現有成員的維度屬性。  
  
-   現有成員的索引鍵。 如果屬性使用複合索引鍵，索引鍵可能需要多個值。  
  
-   並未像其他的屬性已實作在維度中，但適用的任何屬性值。 這樣的屬性包括一元運算、翻譯、自訂積存、自訂積存屬性以及略過的層級。  
  
 **更新**命令使用只有三個必要的屬性：  
  
-   **物件**屬性，其中包含成員要更新之維度的物件參考。 物件參考包含資料庫識別碼、Cube 識別碼以及維度的維度識別碼。  
  
-   **屬性**屬性，其中包含一或多個**屬性**元素，以識別成員要更新的屬性。 **屬性**項目將屬性識別、 提供名稱、 值、 翻譯、 一元運算子、 自訂積存、 自訂積存屬性以及略過更新為識別屬性的單一成員的層級。  
  
    > [!NOTE]  
    >  所有屬性**屬性**必須包含項目。 否則，系統可能會發生錯誤。  
  
-   [其中](../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)屬性，其中包含一或多個**屬性**限制成員要更新的屬性的項目。 **其中**屬性是重要限制**更新**命令成員的特定執行個體。 如果**其中**屬性沒有指定，則會更新指定成員的所有執行個體。 例如，您要將三個客戶的城市名稱從 Redmond 變更為 Bellevue。 若要變更城市名稱，您必須提供**其中**City 屬性中的成員應該變更屬性的識別客戶的三個成員的屬性。 如果您未提供此**其中**屬性，其城市名稱目前為 Redmond 的每個客戶會有縣 （市） 名稱都將變成 Bellevue 之後**更新**命令執行。  
  
    > [!NOTE]  
    >  新的成員，除了**更新**命令只能更新中不包含屬性的屬性機碼值**其中**子句。 例如，更新客戶時無法更新城市名稱，否則會為所有客戶變更城市名稱。  
  
### <a name="updating-members-in-parent-attributes"></a>更新父屬性中的成員  
 為了支援父屬性**更新**命令有選擇性[MoveWithDescendants](../../analysis-services/xmla/xml-elements-properties/movewithdescendants-element-xmla.md)MovewithDescedants 屬性。 設定**MoveWithDescendants**屬性設定為 true 表示父成員之下階應該也能移動與父成員的識別碼，該父成員的變更時。 如果這個值是設定為 false，移動父成員會造成該父成員的直接下階升級為父成員先前所在的層級。  
  
 中父屬性，更新成員時**更新**命令不能更新其他屬性中的成員。  
  
## <a name="dropping-existing-members"></a>卸除現有的成員  
 建構前**卸除**命令時，您應該有可用於卸除成員的下列資訊：  
  
-   要在其中卸除現有成員的維度。  
  
-   要在其中卸除現有成員的維度屬性。  
  
-   要卸除之現有成員的索引鍵。 如果屬性使用複合索引鍵，索引鍵可能需要多個值。  
  
 **卸除**命令使用只有兩個必要的屬性：  
  
-   **物件**屬性，其中包含成員要卸除之維度的物件參考。 物件參考包含資料庫識別碼、Cube 識別碼以及維度的維度識別碼。  
  
-   **其中**屬性，其中包含一或多個**屬性**限制的屬性成員要刪除的項目。 **其中**屬性是重要限制**卸除**命令成員的特定執行個體。 如果**其中**命令未指定，會卸除指定成員的所有執行個體。 例如，您要從 Redmond 卸除三個客戶。 若要卸除這些客戶，您必須提供**其中**屬性以識別 Customer 屬性中要移除的三個成員和三個客戶要從中移除的 City 屬性之 Redmond 成員。 如果**其中**屬性只指定 City 屬性之 Redmond 成員，會卸除與 Redmond 關聯的每個客戶的**卸除**命令。 如果**其中**屬性只在 Customer 屬性中指定的三個成員，這三個客戶便刪除完全由**卸除**命令。  
  
    > [!NOTE]  
    >  **屬性**中包含的項目**卸除**命令必須只包含**AttributeName**和**金鑰**屬性。 否則，系統可能會發生錯誤。  
  
### <a name="dropping-members-in-parent-attributes"></a>卸除父屬性中的成員  
 設定[DeleteWithDescendants](../../analysis-services/xmla/xml-elements-properties/deletewithdescendants-element-xmla.md)屬性表示的父成員下階也應該刪除與父成員。 如果這個值是設定為 false，則會改將父成員的直接下階升級為父成員先前所在的層級。  
  
> [!IMPORTANT]  
>  使用者只要擁有父成員的刪除權限，即可同時刪除父成員及其子階。 使用者不需要子階的刪除權限。  
  
## <a name="see-also"></a>請參閱  
 [卸除元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [插入項目 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Update 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [定義和識別物件 &#40;XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)   
 [在 Analysis Services 中使用 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
