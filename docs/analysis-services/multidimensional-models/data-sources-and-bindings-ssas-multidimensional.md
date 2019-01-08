---
title: 資料來源和繫結 (SSAS 多維度) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 76afbfcd2cd7668cfc65fc5078a1015ac33bc964
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529113"
---
# <a name="data-sources-and-bindings-ssas-multidimensional"></a>資料來源和繫結 (SSAS 多維度)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Cube、維度和其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件都可繫結至資料來源。 資料來源可為下列其中一個物件：  
  
-   關聯式資料來源。  
  
-   輸出一個資料列集 (或多個已編製章節的資料列集) 的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管線。  
  
 這表示，資料來源的表示會因資料來源的類型而有所不同。 例如，關聯式資料來源會以連接字串來區分。 如需資料來源的詳細資訊，請參閱 [多維度模型中的資料來源](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)。  
  
 不論使用的資料來源為何，資料來源檢視 (DSV) 都包含資料來源的中繼資料。 因此，Cube 或其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的繫結會表示為 DSV 的繫結。 這些繫結可以包含繫結，例如檢視、 計算結果的欄和未實際存在於資料來源的關聯性的邏輯物件物件。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將封裝此運算式的導出資料行加入 DSV，然後將對應的 OLAP 量值繫結至 DSV 中的該資料行。 如需 DSV 的詳細資訊，請參閱 [多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)。  
  
 每一個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件都會以它自己的方式繫結至資料來源。 此外，可以使用符合資料繫結物件定義 (如維度) 的方式提供這些物件的資料繫結及資料來源的定義，或是以不符合的方式提供一組個別的定義。  
  
## <a name="analysis-services-data-types"></a>Analysis Services 資料類型  
 繫結中所用的資料類型必須與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]所支援的資料類型相符。 下列資料類型定義於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中：  
  
|Analysis Services 資料類型|描述|  
|---------------------------------|-----------------|  
|BigInt|64 位元帶正負號的整數。 這個資料類型會對應至 Microsoft [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 Int64 資料類型和 OLE DB 內部的 DBTYPE_I8 資料類型。|  
|Bool|布林值 (Boolean)。 這個資料類型會對應至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 Boolean 資料類型和 OLE DB 內部的 DBTYPE_BOOL 資料類型。|  
|CURRENCY|貨幣值，範圍從 -263 (或 -922,337,203,685,477.5808) 到 263-1 (或 +922,337,203,685,477.5807)，正確率為貨幣單位的千分之十。 這個資料類型會對應至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 Decimal 資料類型和 OLE DB 內部的 DBTYPE_CY 資料類型。|  
|date|儲存成雙精確度浮點數的日期資料。 整數部分為自 1899 年 12 月 30 日起的天數，而分數部分則為一天的分數部分。 這個資料類型會對應至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 DateTime 資料類型和 OLE DB 內部的 DBTYPE_DATE 資料類型。|  
|Double|在 -1.79E +308 到 1.79E +308 範圍中的雙精確度浮點數。 這個資料類型會對應至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 Double 資料類型和 OLE DB 內部的 DBTYPE_R8 資料類型。|  
|Integer|32 位元帶正負號的整數。 這個資料類型會對應至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 Int32 資料類型和 OLE DB 內部的 DBTYPE_I4 資料類型。|  
|Single|在 -3.40E +38 到 3.40E +38 範圍中的單精確度浮點數。 這個資料類型會對應至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 Single 資料類型和 OLE DB 內部的 DBTYPE_R4 資料類型。|  
|SmallInt|16 位元帶正負號的整數。 這個資料類型會對應至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 Int16 資料類型和 OLE DB 內部的 DBTYPE_I2 資料類型。|  
|TinyInt|8 位元帶正負號的整數。 這個資料類型會對應至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 SByte 資料類型和 OLE DB 內部的 DBTYPE_I1 資料類型。<br /><br /> 注意：如果資料來源包含屬於 Tinyint 資料類型的欄位，且 AutoIncrement 屬性設為 True，則它們會在資料來源檢視中轉換為整數。|  
|UnsignedBigInt|64 位元不帶正負號的整數。 這個資料類型會對應至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 UInt64 資料類型和 OLE DB 內部的 DBTYPE_UI8 資料類型。|  
|UnsignedInt|32 位元不帶正負號的整數。 這個資料類型會對應至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 UInt32 資料類型和 OLE DB 內部的 DBTYPE_UI4 資料類型。|  
|UnsignedSmallInt|16 位元不帶正負號的整數。 這個資料類型會對應至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 UInt16 資料類型和 OLE DB 內部的 DBTYPE_UI2 資料類型。|  
|WChar|Unicode 字元的以 Null 結束資料流。 這個資料類型會對應至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 內部的 String 資料類型和 OLE DB 內部的 DBTYPE_WSTR 資料類型。|  
  
 所有從資料來源收到的資料都會轉換成繫結中指定 (通常在處理期間指定) 的 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 類型。 如果無法執行轉換 (例如從 String 轉換成 Int)，就會引發錯誤。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 通常會將繫結中的資料類型設定為最符合資料來源中來源類型的資料類型。 例如，SQL 類型 Date、DateTime、SmallDateTime、DateTime2 和 DateTimeOffset 會對應至 [!INCLUDE[ssAS](../../includes/ssas-md.md)] Date，而 SQL 類型 Time 則會對應至 String。  
  
## <a name="bindings-for-dimensions"></a>維度的繫結  
 維度的每一個屬性都會繫結至 DSV 中的資料行。 維度的所有屬性都必須來自於單一資料來源。 但是，屬性可繫結至不同資料表中的資料行。 資料表之間的關聯性會定義在 DSV 中。 在相同資料表的一組以上的關聯性存在的情況下，可能必須導入做為 「 別名 」 資料表 DSV 中的具名的查詢。 運算式和篩選會使用具名計算和具名查詢定義在 DSV 中。  
  
## <a name="bindings-for-measuregroups-measures-and-partitions"></a>量值群組、量值和資料分割的繫結  
 每個量值群組都有下列預設繫結：  
  
-   量值群組會繫結至 DSV 中的資料表 (例如 **MeasureGroup.Source**)。  
  
-   每一個量值都會繫結至該資料表中的資料行 (例如 **Measure.ValueColumn.Source**)。  
  
-   每一個量值群組維度都有一組「資料粒度屬性」可定義此量值群組的資料粒度。 每一個屬性都必須繫結至包含此屬性索引鍵之事實資料表中的一或多個資料行  (如需有關資料粒度屬性的詳細資訊，請參閱本主題稍後的「量值群組資料粒度屬性」)。  
  
 可以根據資料分割選擇性地覆寫這些預設繫結。 每一個資料分割都可以指定不同的資料來源、資料表或查詢名稱，或是篩選運算式。 最常見的資料分割策略是使用相同的資料來源，根據資料分割覆寫資料表。 替代方式包括根據資料分割套用不同的篩選，或是變更資料來源。  
  
 預設資料來源必須定義於 DSV 中，藉此提供結構描述資訊，包括關聯性的詳細資料在內。 在資料分割層級上指定的任何其他資料表或查詢都不需要列在 DSV 中，但是它們的結構描述必須與針對量值群組定義之預測資料表的結構描述相同，或是至少必須包含量值或資料粒度屬性所使用的所有資料行。 根據量值的詳細繫結及資料粒度屬性無法在資料分割層級上覆寫，而且會假設它們是針對量值群組所定義的相同資料行。 因此，如果資料分割使用的資料來源事實上有不同的結構描述，則為此資料分割定義的 **TableDefinition** 查詢必須產生與量值群組使用之結構描述相同的結構描述。  
  
### <a name="measuregroup-granularity-attributes"></a>量值群組資料粒度屬性  
 當量值群組的資料粒度符合資料庫中已知的資料粒度，而且事實資料表與維度資料表之間有直接關聯性時，資料粒度屬性只需要繫結至事實資料表上的適當外部索引鍵資料行。 例如，假設有以下的事實資料表和維度資料表：  
  
 `Sales(RequestedDate, OrderedProductID, ReplacementProductID, Qty)`  
  
 `Product(ProductID, ProductName,Category)`  
  
 ``  
  
 `Relation: Sales.OrderedProductID -> Product.ProductID`  
  
 `Relation: Sales.ReplacementProductID -> Product.ProductID`  
  
 ``  
  
 如果您針對 Sales 維度角色上的 Ordered Product，依排序產品進行分析，則 Product 資料粒度屬性會繫結至 Sales.OrderedProductID。  
  
 但是， **GranularityAttributes** 有可能不會以資料行的形式存在於事實資料表上。 例如在下列情況下， **GranularityAttributes** 可能不會以資料行的形式存在：  
  
-   OLAP 資料粒度比來源的資料粒度較粗。  
  
-   中繼資料表會介入事實資料表與維度資料表之間。  
  
-   維度索引鍵與維度資料表中的主索引鍵不同。  
  
 在所有的這類情況中，必須定義 DSV，好讓 GranularityAttributes 存在於事實資料表上。 例如，可以導入具名查詢或導出資料行。  
  
 例如，在與上面相同的範例資料表中，如果資料粒度是依據 Category，則可能會導入 Sales 的檢視：  
  
 `SalesWithCategory(RequestedDate, OrderedProductID, ReplacementProductID, Qty, OrderedProductCategory)`  
  
 `SELECT Sales.*, Product.Category AS OrderedProductCategory`  
  
 `FROM Sales INNER JOIN Product`  
  
 `ON Sales.OrderedProductID = Product.ProductID`  
  
 ``  
  
 在此情況下，GranularityAttribute Category 會繫結至 SalesWithCategory.OrderedProductCategory。  
  
### <a name="migrating-from-decision-support-objects"></a>從 Decision Support Objects 移轉  
 Decision Support Objects (DSO) 8.0 允許重新繫結 **PartitionMeasures** 。 因此，這些情況下的移轉策略是要建構適當的查詢。  
  
 同樣地，重新繫結資料分割內的維度屬性是不可行的，雖然 DSO 8.0 也允許這個重新繫結。 這些情況下的移轉策略是在 DSV 中定義必要的具名查詢，好讓資料分割之 DSV 中存在的資料表和資料行與用於此維度的資料表和資料行相同。 這些情況可能需要採用簡單的移轉，也就是將 From/Join/Filter 子句對應到單一具名查詢，而不是一組結構化相關資料表。 因為即使資料分割使用相同的資料來源，DSO 8.0 還是允許重新繫結 PartitionDimensions，所以移轉可能會要求相同的資料來源有多個 DSV。  
  
 在 DSO 8.0 中，對應的繫結可用兩個不同方式來表示，這是取決於是否利用最佳化結構描述 (其方式是繫結至維度資料表上的主索引鍵或是事實資料表上的外部索引鍵)。 在 ASSL 中，不會區別兩個不同的格式。  
  
 即使是針對使用了未包含維度資料表之資料來源的資料分割，還是會套用相同的繫結方式，因為繫結是針對事實資料表中的外部索引鍵資料行，而不是針對維度資料表中的主索引鍵資料行。  
  
## <a name="bindings-for-mining-models"></a>採礦模型的繫結  
 採礦模型是關聯式或 OLAP。 關聯式採礦模型的資料繫結與 OLAP 採礦模型的繫結有很大的不同。  
  
### <a name="bindings-for-a-relational-mining-model"></a>關聯式採礦模型的繫結  
 關聯式採礦模型會依賴 DSV 中定義的關聯性，以解決有關哪些資料行繫結至哪些資料來源的任何模稜兩可情況。 在關聯式採礦模型中，資料繫結會遵循以下規則：  
  
-   每一個非巢狀資料表資料行都會繫結至案例資料表上或與案例資料表相關之資料表上的資料行 (遵循多對一或一對一關聯性)。 DSV 會定義資料表之間的關聯性。  
  
-   每個巢狀資料表資料行都會繫結至來源資料表。 這些資料行會由巢狀資料表資料行所擁有，然後繫結至該來源資料表上或與來源資料表相關之資料表上的資料行  (此繫結同樣會遵循多對一或一對一關聯性)。採礦模型繫結不會提供巢狀資料表的聯結路徑。 但是，DSV 中定義的關聯性會提供這項資訊。  
  
### <a name="bindings-for-an-olap-mining-model"></a>OLAP 採礦模型的繫結  
 OLAP 採礦模型沒有與 DSV 同等的項目。 因此，資料繫結必須提供資料行與資料來源之間的任何去除混淆內容。 例如，採礦模型可以根據 Sales Cube，而資料行可以根據 Qty、Amount 和 Product Name。 另外，採礦模型也可以根據 Product，而資料行可以根據 Product Name、Product Color 和具有 Sales Qty 的巢狀資料表。  
  
 在 OLAP 採礦模型中，資料繫結會遵循以下規則：  
  
-   每一個非巢狀資料表資料行都會繫結至 Cube 上的量值、該 Cube 之維度上的屬性 (如果是維度角色，則會指定 **CubeDimension** 來讓意義明確)，或是維度上的屬性。  
  
-   每個巢狀資料表資料行都會繫結至 **CubeDimension**。 也就是說，它會定義如何從維度導覽至相關 Cube 或是 (在比較不常見的巢狀資料表案例中) 從 Cube 導覽至它的其中一個維度。  
  
## <a name="out-of-line-bindings"></a>非正規 (Out-of-Line) 繫結  
 非正規繫結可讓您在命令的持續期間暫時變更現有的資料繫結。 非正規繫結指的是命令中已包含但是未保存的繫結。 只有在執行該特定命令時，才會套用非正規繫結。 相較之下，正規繫結會包含在 ASSL 物件定義中，並且與物件定義一起保存在伺服器中繼資料中。  
  
 ASSL 允許在 **Process** 命令上 (如果不在批次中) 或 **Batch** 命令上指定非正規繫結。 如果在 **Batch** 命令上指定非正規繫結，所有在 **Batch** 命令中指定的繫結都會在批次執行的所有 **Process** 命令中建立新的繫結內容。 這個新的繫結內容包含由於 **Process** 命令所間接處理的物件。  
  
 在命令上指定非正規繫結時，它們會覆寫針對指定物件保存之 DDL 中的正規繫結。 這些處理過的物件可能會包含 **Process** 命令中直接命名的物件，或者可能包含在處理過程中自動起始處理的其他物件。  
  
 非正規繫結的指定方式，是使用處理命令來包含選擇性 **Bindings** 集合物件。 選擇性 **Bindings** 集合包含下列元素。  
  
|屬性|基數|類型|描述|  
|--------------|-----------------|----------|-----------------|  
|**繫結**|0-n|**繫結**|提供新繫結的集合。|  
|**DataSource**|0-1|**DataSource**|取代原本會使用之伺服器中的 **DataSource** 。|  
|**DataSourceView**|0-1|**DataSourceView**|取代原本會使用之伺服器中的 **DataSourceView**<br /><br /> 。|  
  
 與非正規繫結相關的所有元素都是選擇性的。 如果是未指定的任何元素，ASSL 會使用保存之物件 DDL 中所包含的指定內容。 **Process** 命令中 **DataSource** 或 **DataSourceView** 的指定是選擇性的。 如果指定了 **DataSource** 或 **DataSourceView** ，則在 **Process** 命令完成之後，不會將它們具現化及保存下來。  
  
### <a name="definition-of-the-out-of-line-binding-type"></a>非正規繫結類型的定義  
 在非正規 **Bindings** 集合內，ASSL 允許多個物件的繫結集合，每一個都是 **Binding**。 每一個 **Binding** 都有擴充物件參考 (類似於物件參考)，但是也可意指次要物件 (例如維度屬性和量值群組屬性)。 這個物件會典型的一般格式**物件**中的項目**程序**命令，除了\<*物件*> \< */物件*> 標記並不存在。  
  
 指定繫結的每個物件都會由 XML 項目表單的\<*物件*> 識別碼 (例如**DimensionID**)。 識別物件之後盡量明確地與表單\<*物件*> 識別碼，您會識別為其已指定繫結，這通常是元素**來源**. 值得注意的常見情況是哪一個 **Source** 是 **DataItem**上的屬性，這是屬性中資料行繫結的情況。 在此情況下，您不會指定 **DataItem** 標記，而只會指定 **Source** 屬性，就像它直接位於要繫結的資料行上一樣。  
  
 **KeyColumns** 是由其在 **KeyColumns** 集合內的順序加以識別。 例如，在這裡無法僅指定屬性的第一和第三個索引鍵資料行，因為沒有方法可以指示要略過第二個索引鍵資料行。 所有的索引鍵資料行都必須位於維度屬性的非正規繫結中。  
  
 **Translations**(雖然沒有識別碼) 會根據其語言來進行語意識別。 因此， **Binding** 內的 **Translations** 必須包含其語言識別碼。  
  
 未直接存在於 DDL 中之 **Binding** 內允許的一個其他元素是 **ParentColumnID**，它會用於資料採礦的巢狀資料表。 在此情況下，在巢狀資料表中識別有提供繫結的父資料行是必要的。  
  
  
