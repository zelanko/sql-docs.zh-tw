---
title: "變更屬性中的資料來源檢視 (Analysis Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- friendly names [Analysis Services]
- names [Analysis Services], data source views
- viewing tables
- displaying tables
- data source views [Analysis Services], tables
- tables [Analysis Services], data source views
ms.assetid: 4ccdabea-9c4d-460d-ba78-d23068143696
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b8d8d731552fe099d161d6b87bca87ceecd709a9
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="change-properties-in-a-data-source-view-analysis-services"></a>變更資料來源檢視的屬性 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]定義資料來源檢視，使用資料來源檢視精靈，以及加入資料表、 檢視、 具名計算和具名的查詢，以資料來源檢視之後，您可能想要變更與相關的屬性：  
  
-   資料來源檢視比對準則  
  
-   進階資料來源檢視選項  
  
-   物件名稱  
  
-   物件中繼資料  
  
 您也可以檢視從無法修改之資料來源中擷取的物件中繼資料。  
  
## <a name="viewing-or-changing-data-source-view-properties"></a>檢視或變更資料來源檢視屬性  
 當您最初定義資料來源檢視時，[資料來源檢視精靈] 會設定資料來源檢視的描述以外的資料來源檢視屬性。 下表列出並描述資料來源檢視的屬性。  
  
> [!NOTE]  
>  [屬性] 窗格顯示 .dsv 檔的屬性，以及 DSV 物件的屬性。 若要檢視此物件的屬性，請在 [方案總管] 中按兩下物件。 [屬性] 將更新以反映下表所顯示的屬性。  
  
|屬性|說明|  
|--------------|-----------------|  
|資料來源|指定您要檢視其屬性之資料來源檢視內的資料來源。|  
|說明|指定資料來源檢視的描述。|  
|名稱|指定出現在 [方案總管] 或 Analysis Services 資料庫中的資料來源檢視名稱。 您可以在這裡或 [方案總管] 中變更此資料來源檢視名稱。|  
|NameMatchingCriteria|資料來源的名稱比對準則； 如果 [資料來源檢視精靈] 偵測到主索引鍵 - 外部索引鍵關聯性，則預設值為 (無)。 不論 [資料來源檢視精靈] 是否有設定這個屬性，您都可以在這裡指定值。 如果有資料庫關聯性存在，而且您有指定名稱比對準則，則這兩者都會用來推斷現有資料表與新加入之資料表之間的關聯性。|  
|RetrieveRelationships|指定是否要從資料庫擷取關聯性。 預設值是 True。|  
|SchemaRestriction|指定對於從資料來源擷取之結構描述的限制 (如果有的話)。 依預設，不會有任何結構描述限制存在。|  
  
## <a name="viewing-or-changing-datatable-properties"></a>檢視或變更 DataTable 屬性  
 **[DataTable]** 屬性是資料來源檢視中資料表、檢視和具名查詢的屬性， 將任何物件加入到資料來源檢視時，會設定這些屬性。 下表列出並描述資料來源檢視中 **[DataTable]** 物件的屬性。  
  
|屬性|說明|  
|--------------|-----------------|  
|AllowChangesDuringGeneration|指定 [結構描述產生精靈] 是否有權限可以在重新產生期間覆寫資料來源檢視資料表； 這個屬性只會存在於最初由 [結構描述產生精靈] 所產生的資料表上。 如需詳細資訊，請參閱 [了解累加式產生](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)。|  
|DataSource|指定物件的資料來源。 您不能編輯這個屬性。|  
|說明|指定資料表、檢視或具名查詢的描述。 如果基礎資料庫資料表或檢視具有儲存為擴充屬性的描述，就會出現這個值。 您可以編輯這個屬性。|  
|FriendlyName|對資料表或檢視指定讓使用者更容易了解的名稱，或是指定與主題領域更有相關性的名稱。 依預設，資料表或檢視的 **[FriendlyName]** 屬性會與資料表或檢視的 **[Name]** 屬性相同。 當根據資料表或檢視來定義物件名稱時，OLAP 和資料採礦物件會使用 **[FriendlyName]** 屬性。 您可以編輯這個屬性。|  
|名稱|指定基礎資料表或檢視的名稱，或是具名查詢的名稱。 當根據具名查詢來定義物件名稱時，OLAP 和資料採礦物件會使用 **[Name]** 屬性。 只有在具名查詢中才可以編輯這個屬性。|  
|QueryDefinition|指定具名查詢定義。 這個屬性只適用於具名查詢，而且不能直接編輯； 若要編輯這個屬性，您要編輯此具名查詢本身。|  
|結構描述|指定適用於資料表、檢視或具名查詢的資料庫結構描述。 無法編輯這個屬性。|  
|TableType|指定資料表、檢視表或具名查詢的資料表類型。 無法編輯這個屬性。|  
  
## <a name="viewing-or-changing-datacolumn-properties"></a>檢視或變更 DataColumn 屬性  
 **[DataColumn]** 屬性是資料來源檢視中資料表、檢視表及具名查詢內資料行的屬性， 當任何物件加入到資料來源檢視 (從基礎資料表或檢視、具名查詢，或是具名計算所定義)，便會設定這些屬性。 下表列出並描述資料來源檢視中 **[DataColumn]** 物件的屬性。  
  
|屬性|說明|  
|--------------|-----------------|  
|AllowNull|根據基礎資料表、值或具名查詢中的資料行來指定資料行的 Null 屬性。 無法編輯這個屬性。|  
|DataType|根據基礎資料表、值或具名查詢中的資料行來指定資料行的資料類型。 無法直接編輯這個屬性， 但是，如果您需要變更資料表或檢視中資料行的資料類型，請使用會將此資料行轉換成所需資料類型的具名查詢來取代此資料表。|  
|DateTimeMode|指定 **[DateTime]** 資料行的日期序列化格式； 預設值為 **[UnspecifiedLocal]**。 可以編輯這個屬性。|  
|說明|指定資料行的描述。 如果基礎資料庫資料行具有儲存為擴充屬性的描述，就會出現這個值。 您可以編輯這個屬性。|  
|FriendlyName|對資料表或檢視中的資料行指定讓使用者更容易了解的名稱，或是指定與主題領域更有相關性的名稱。 依預設，資料表或檢視中資料行的 **[FriendlyName]** 屬性會與該資料行的 **[Name]** 屬性相同。 當根據資料表或檢視中的資料行來定義屬性時，OLAP 和資料採礦物件會使用 **[FriendlyName]** 屬性。 您可以編輯這個屬性。|  
|長度|根據基礎資料表或檢視中資料行內的資料來指定資料行的最大長度。|  
|名稱|指定基礎資料行的名稱，或是具名計算的名稱。 當根據具名計算來定義屬性時，OLAP 和資料採礦物件會使用 **[Name]** 屬性。 只有在具名計算中才可以編輯這個屬性。|  
  
## <a name="see-also"></a>請參閱  
 [多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [在資料來源檢視設計工具中使用圖表 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  
