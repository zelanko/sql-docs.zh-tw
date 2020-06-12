---
title: ASSL XML 慣例 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- whitespace [Analysis Services Scripting Language]
- trailing whitespace
- XSD data types [Analysis Services Scripting Language]
- inheritance [Analysis Services Scripting Language]
- cardinality [Analysis Services Scripting Language]
- white space [Analysis Services Scripting Language]
- ASSL, XML conventions
- defaults [Analysis Services Scripting Language]
- leading whitespace
- Analysis Services Scripting Language, XML conventions
- XML [Analysis Services Scripting Language]
- hierarchies [Analysis Services Scripting Language]
- inherited defaults [Analysis Services Scripting Language]
ms.assetid: bce4edad-4420-41ce-9672-8c00c5c0dec6
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9b70742b07fd6450b01cf205147a05f40c4b6121
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545670"
---
# <a name="assl-xml-conventions"></a>ASSL XML 慣例
  Analysis Services 指令碼語言 (ASSL) 將物件階層以一組元素類型來表示，每個元素類型都定義了它們可以包含的子系元素。  
  
 為了表示物件階層，ASSL 使用下列 XML 慣例：  
  
-   所有物件和屬性都是以元素表示，但標準 XML 屬性（例如 ' XML： lang '）除外。  
  
-   元素名稱與列舉值都會遵循 Microsoft .NET Framework 所採用之 Pascal 大小寫 (不使用底線) 的命名慣例。  
  
-   所有值的大小寫都會保留。 列舉值也會區分大小寫。  
  
 除了這個慣例清單以外，Analysis Services 也會遵循有關基數、繼承、空白、資料類型以及預設值的某些慣例。  
  
## <a name="cardinality"></a>基數  
 當元素具有大於 1 的基數時，就會有封裝此元素的 XML 元素集合。 集合名稱會使用包含在集合中的複數形式之元素。 例如，下列 XML 區段代表 `Dimensions` 元素中的 `Database` 集合：  
  
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
 當有不同的物件具有重疊但非常不一樣的屬性集合時，就會使用繼承。 像這類重疊但是相異的物件為虛擬 Cube、連結 Cube 以及一般 Cube。 對於重疊但是相異的物件，Analysis Services 會使用 XML 執行個體命名空間的標準 `type` 屬性來指出繼承。 例如，下列 XML 片段示範 `type` 屬性如何識別 `Cube` 元素是繼承自正規 Cube 或繼承自虛擬 Cube：  
  
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
  
 當多個類型都具有相同名稱的屬性時，通常不會使用繼承。 例如，`Name` 與 `ID` 屬性出現在許多元素上，但是這些屬性尚未升級到抽象類型。  
  
## <a name="whitespace"></a>空白  
 元素值中的空白會保留下來。 不過，開頭和尾端空白則一律都會修剪。 例如，下列元素有相同的文字，但是在文字中有不同的空白數目，因此會將它們視為不同的值：  
  
 `<Description>My text<Description>`  
  
 `<Description>My  text<Description>`  
  
 ``  
  
 不過，下列元素只有開頭和尾端空白不同，因此會將它們視為具有相等的值：  
  
 `<Description>My text<Description>`  
  
 `<Description>  My text  <Description>`  
  
 ``  
  
## <a name="data-types"></a>資料類型  
 Analysis Services 使用下列標準 XML 結構描述定義語言 (XSD) 資料類型：  
  
 `Int`  
 介於-231 到 231-1 範圍的整數值。  
  
 `Long`  
 介於-263 到 263-1 範圍的整數值。  
  
 `String`  
 符合下列全域規則的字串值：  
  
-   移除控制字元。  
  
-   修剪開頭和尾端空白。  
  
-   保留內部空白字元。  
  
 `Name` 與 `ID` 屬性對於字串元素中的有效字元具有特殊限制。 如需和慣例的詳細資訊 `Name` `ID` ，請參閱[ASSL 物件和物件特性](assl-objects-and-object-characteristics.md)。  
  
 `DateTime`  
 `DateTime`.NET Framework 中的結構。  值不可以是 NULL。 `DataTime` 資料類型支援的最低日期是 1601 年 1 月 1 日，可供程式設計人員做為 `DateTime.MinValue` 來使用。 出現支援的最低日期即表示您遺漏了 `DateTime` 值。  
  
 `Boolean`  
 只有兩個值的列舉，例如 {true, false} 或是 {0, 1}。  
  
## <a name="default-values"></a>預設值  
 Analysis Services 會使用下表所列的預設值。  
  
|XML 資料類型|預設值|  
|-------------------|-------------------|  
|`Boolean`|False|  
|`String`|"" (空字串)|  
|`Integer` 或 `Long`|0 (零)|  
|`Timestamp`|12:00:00 AM、1/1/0001 （對應至0刻度的 .NET Framework `System.DateTime` ）|  
  
 有顯示但為空的元素會解譯成具有 Null 字串值，而不是預設值。  
  
### <a name="inherited-defaults"></a>繼承的預設值  
 物件上指定的某些屬性會針對子物件或下階物件上的相同屬性提供預設值。 例如，`Cube.StorageMode` 會針對 `Partition.StorageMode` 提供預設值。 Analysis Services 套用於繼承預設值的規則如下所示：  
  
-   當子物件的屬性在 XML 中為 Null 時，其值就會預設為繼承的值。 但是，如果您從伺服器查詢此值，伺服器會傳回 XML 元素的 null 值。  
  
-   您無法以程式設計方式判斷出子物件的屬性是直接在子物件上設定的，還是繼承而來。  
  
 有些元素已定義遺漏元素時會套用的預設值。 例如，在下列 XML 片段中，即使當某個 `Dimension` 元素包含 `Dimension` 元素，但是另一個 `Visible` 元素不包含時，`Dimension` 元素也是相等的。  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 如需繼承預設值的詳細資訊，請參閱[ASSL 物件和物件特性](assl-objects-and-object-characteristics.md)。  
  
  
