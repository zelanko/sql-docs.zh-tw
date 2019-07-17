---
title: ASSL XML 慣例 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c357efe4636c1b502cdb57305b9072907d4b2e98
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165214"
---
# <a name="assl-xml-conventions"></a>ASSL XML 慣例
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services 指令碼語言 (ASSL) 將物件階層以一組元素類型來表示，每個元素類型都定義了它們可以包含的子系元素。  
  
 為了表示物件階層，ASSL 使用下列 XML 慣例：  
  
-   所有物件和屬性都被都以項目，但 'xml: lang' 等標準 XML 屬性除外。  
  
-   元素名稱與列舉值的 Microsoft.NET Framework 命名慣例的 pascal 命名法大小寫不使用底線。  
  
-   所有值的大小寫都會保留。 列舉值也會區分大小寫。  
  
 除了這個慣例清單以外，Analysis Services 也會遵循有關基數、繼承、空白、資料類型以及預設值的某些慣例。  
  
## <a name="cardinality"></a>基數  
 當元素具有大於 1 的基數時，就會有封裝此元素的 XML 元素集合。 集合名稱會使用包含在集合中的複數形式之元素。 例如，下列 XML 片段表示**維度**內的集合**資料庫**項目：  
  
 `<Database>`  
  
 `...`  
  
 `<Dimensions>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `</Dimensions>`  
  
 `</Database>`  
  
 ``  
  
 元素出現的順序並不重要。  
  
## <a name="inheritance"></a>繼承  
 當有不同的物件具有重疊但非常不一樣的屬性集合時，就會使用繼承。 像這類重疊但是相異的物件為虛擬 Cube、連結 Cube 以及一般 Cube。 對於重疊但是相異的物件，Analysis Services 會使用標準**型別**XML 執行個體命名空間，來指出繼承屬性。 例如，下列 XML 程式碼片段示範如何**型別**屬性會識別是否**Cube**元素繼承自正規 cube 或從虛擬 cube:  
  
 `<Cubes>`  
  
 `<Cube xsi:type="RegularCube">`  
  
 `<Name>Sales</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `<Cube xsi:type="VirtualCube">`  
  
 `<Name>SalesAndInventory</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `</Cubes>`  
  
 ``  
  
 當多個類型都具有相同名稱的屬性時，通常不會使用繼承。 例如，**名稱**並**識別碼**許多項目，會顯示屬性，但這些屬性尚未升級到抽象類型。  
  
## <a name="whitespace"></a>空白  
 元素值中的空白會保留下來。 不過，開頭和尾端空白則一律都會修剪。 例如，下列元素有相同的文字，但是在文字中有不同的空白數目，因此會將它們視為不同的值：  
  
 `<Description>My text<Description>`  
  
 `<Description>My  text<Description>`  
  
 ``  
  
 不過，下列元素只有開頭和尾端空白不同，因此會將它們視為具有相等的值：  
  
 `<Description>My text<Description>`  
  
 `<Description>  My text  <Description>`  
  
 ``  
  
## <a name="data-types"></a>資料型別  
 Analysis Services 使用下列標準 XML 結構描述定義語言 (XSD) 資料類型：  
  
 **整數**  
 -231 到 231-1 的範圍中整數值。  
  
 **Long**  
 -263 到 263-1 的範圍中整數值。  
  
 **String**  
 符合下列全域規則的字串值：  
  
-   移除控制字元。  
  
-   修剪開頭和尾端空白。  
  
-   保留內部空白字元。  
  
 **名稱**並**識別碼**屬性的字串項目中的有效字元有特殊限制。 如需詳細資訊**名稱**並**識別碼**慣例，請參閱[ASSL 物件和物件特性](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)。  
  
 **DateTime**  
 A **DateTime**從.NET Framework 的結構。 A **DateTime**值不能是 NULL。 所支援的最低日期**DataTime**資料類型是 1601 年 1 月 1 日起，這是供做為程式設計人員**DateTime.MinValue**。 支援的最低日期表示**DateTime**遺漏值。  
  
 **布林**  
 只有兩個值的列舉，例如 {true, false} 或是 {0, 1}。  
  
## <a name="default-values"></a>預設值  
 Analysis Services 會使用下表所列的預設值。  
  
|XML 資料類型|預設值|  
|-------------------|-------------------|  
|**布林**|False|  
|**String**|"" (空字串)|  
|**整數**或**長**|0 (零)|  
|**時間戳記**|12:00:00 AM，1/1/0001 (對應至.NET Frameworks **System.DateTime** 0 刻度)|  
  
 有顯示但為空的元素會解譯成具有 Null 字串值，而不是預設值。  
  
### <a name="inherited-defaults"></a>繼承的預設值  
 物件上指定的某些屬性會針對子物件或下階物件上的相同屬性提供預設值。 例如， **Cube.StorageMode**提供的預設值**Partition.StorageMode**。 Analysis Services 套用於繼承預設值的規則如下所示：  
  
-   當子物件的屬性在 XML 中為 Null 時，其值就會預設為繼承的值。 但是，如果您從伺服器查詢此值，伺服器會傳回 XML 元素的 null 值。  
  
-   您無法以程式設計方式判斷出子物件的屬性是直接在子物件上設定的，還是繼承而來。  
  
 有些元素已定義遺漏元素時會套用的預設值。 例如，**維度**下列 XML 片段中的項目都相等，即使當某個**維度**項目包含**看得見**項目，但是其他**維度**項目則否。  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 如需有關繼承的預設值的詳細資訊，請參閱 < [ASSL 物件和物件特性](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)。  
  
  
