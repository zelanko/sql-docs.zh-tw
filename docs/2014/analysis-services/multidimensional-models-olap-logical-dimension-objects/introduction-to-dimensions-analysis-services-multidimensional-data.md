---
title: 維度簡介（Analysis Services 多維資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], about dimensions
- storage [Analysis Services], dimensions
- dimensions [Analysis Services], examples
- storing data [Analysis Services], dimensions
- storage [Analysis Services]
ms.assetid: ab170fdd-4144-42db-9497-690b9189fc25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1a78735cd5aee5ebc87adaac6fab48bb4e183d6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81387898"
---
# <a name="introduction-to-dimensions-analysis-services---multidimensional-data"></a>維度簡介 (Analysis Services - 多維度資料)
  所有的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Microsoft 維度都是根據資料來源視圖中資料表或 views 的資料行所組成的屬性群組。 維度的存在與 Cube 無關，也可以用於多個 Cube 中、在單一 Cube 中使用多次，也可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之間連結。 存在與 Cube 無關的維度稱為資料庫維度，而 Cube 中的資料庫維度執行個體則稱為 Cube 維度。  
  
## <a name="dimension-based-on-a-star-schema-design"></a>根據星狀結構描述設計的維度  
 維度的結構主要是由基礎維度資料表或資料表的結構來驅動。 最簡單的結構稱為星狀結構描述，其中的每個維度都會根據單一維度資料表，而該資料表又會透過「主索引鍵 - 外部索引鍵」關聯性直接連結至事實資料表。  
  
 [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)]下圖說明範例資料庫的子區段，其中**FactResellerSales**事實資料表與兩個維度資料表**DimReseller**和**dimpromotion 這**相關。 **FactResellerSales**事實資料表中的**ResellerKey**資料行，會定義與**DimReseller**維度資料表中**ResellerKey**主鍵資料行的外鍵關聯性。 同樣地， **FactResellerSales**事實資料表中的**PromotionKey**資料行也會定義與**dimpromotion 這**維度資料表中**PromotionKey**主鍵資料行的外鍵關聯性。  
  
 ![事實維度關聯性的邏輯結構描述](../../analysis-services/dev-guide/media/dimfactrelationship.gif "事實維度關聯性的邏輯結構描述")  
  
## <a name="dimension-based-on-a-snowflake-schema-design"></a>根據雪花式結構描述設計的維度  
 一般而言，會需要較複雜的結構，因為定義維度時需要有來自多個資料表的資訊。 在這個結構 (稱為雪花式結構描述) 中，每一個維度會以多個互相連結之資料表中資料行內的屬性為基礎，而最後會依「主索引鍵 - 外部索引鍵」關聯性連結至事實資料表。 例如，下圖說明在**AdventureWorksDW**範例專案中，完整描述產品維度所需的資料表：  
  
 ![AdventureWorksAS 產品維度的資料表](../../analysis-services/dev-guide/media/dimproduct.gif "AdventureWorksAS 產品維度的資料表")  
  
 若要完整地描述產品，產品的類別目錄與子類別目錄必須包含在產品維度中。 不過，該資訊並不會直接存放在**DimProduct**維度的主資料表中。 從**DimProduct**到**DimProductSubcategory**的外鍵關聯性（後者與**DimProductCategory**資料表的外鍵關聯性），可以在 product 維度中包含產品類別目錄和子類別的資訊。  
  
## <a name="snowflake-schema-versus-reference-relationship"></a>雪花式結構描述與參考關聯性的比較  
 有時您可以選擇使用雪花式結構描述，從多份資料表中定義維度中的屬性，或選擇定義兩個不同的維度，然後定義它們之間的參考維度關聯性。 下列圖表說明如此的狀況。  
  
 ![範例參考維度的邏輯結構描述](../../analysis-services/dev-guide/media/dimindirect.gif "範例參考維度的邏輯結構描述")  
  
 在上圖中， **FactResellerSales**事實資料表與**DimGeography**維度資料表沒有外鍵關聯性。 不過， **FactResellerSales**事實資料表與**DimReseller**維度資料表具有外鍵關聯性，而後者又與**DimGeography**維度資料表具有外鍵關聯性。 若要定義「轉售商」維度，其中包含每個轉銷商的地理資訊，您必須從**DimGeography**和**DimReseller**維度資料表中取出這些屬性。 然而，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，您可以建立兩個個別的維度，然後在這兩個維度之間定義參考維度關聯性，以在量值群組中連結它們，因而獲得相同的結果。 如需參考維度關聯性的詳細資訊，請參閱[維度關聯](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)性。  
  
 在這個狀況下使用參考維度關聯性的其中一個好處是您可以建立單一地理位置維度，然後根據地理位置維度建立多個 Cube 維度，而完全不需要任何額外的儲存空間。 例如，您可以將一個地理位置 Cube 維度連結至轉售商維度，而將另一個地理位置 Cube 維度連結至客戶維度。 **相關主題：**[維度關聯](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)性、[定義參考的關聯性及參考的關聯性屬性](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)  
  
## <a name="processing-a-dimension"></a>處理維度  
 建立維度之後，您必須先處理維度，才能檢視屬性的成員與維度中的階層。 變更維度的結構或更新其基礎資料表中的資訊之後，必須再次處理此維度，然後才可以檢視這些變更。 在結構性變更之後處理維度時，也必須處理包含此維度的任何 Cube，否則將無法檢視此 Cube。  
  
## <a name="security"></a>安全性  
 維度的所有從屬物件，包括階層、層級和成員，都是使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的角色來保護。 維度安全性可套用至資料庫中使用該維度的所有 Cube，或只套用至特定 Cube。 如需維度安全性的詳細資訊，請參閱[授與維度的許可權 &#40;Analysis Services&#41;](../multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [維度儲存體](../multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [維度翻譯](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [可寫入維度](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
