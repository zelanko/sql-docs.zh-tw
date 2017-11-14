---
title: "CSDLBI 概念 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 2fbdf621-a94d-4a55-a088-3d56d65016ac
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0b38e5f9de0860c75c0262c2e9684cc5440ba22d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="csdlbi-concepts"></a>CSDLBI 概念

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  具有 BI 註解的概念結構定義語言 (CSDLBI) 是以實體資料架構為基礎，這是一種用於表示資料摘要，以便用程式設計方式存取、查詢或匯出不同的資料集。 CSDLBI 可用來表示使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 建立的資料模型，因為它支援豐富的資料驅動報表和應用程式。  
  
 本節將說明 CSDLBI 表示法如何對應 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料模型 (包含表格式與多維度)，以及每個模型類型的範例。  
  
 用來說明這些概念的範例都取自 AdventureWorks 範例資料庫 (可在 Codeplex 上取得)。 如需這些範例的詳細資訊，請參閱[SQL Server 的 Adventure Works 範例](http://go.microsoft.com/fwlink/?linkID=220093)。  
  
## <a name="structure-of-a-tabular-model-in-csdlbi"></a>CSDLBI 中表格式模型的結構  
 描述報表模型及其資料的 CSDLBI 文件會以 xsd 陳述式為開頭，後面接著模型的定義。  
  
 模型是一種命名空間，其中包含下列主要實體、關聯和屬性：  
  
-   **EntityContainer**列出模型中的資料表。  
  
-   列出的每個資料表都會**EntityContainer**為**EntitySet**。  
  
-   兩個資料表之間每個關聯性描述為**AssociationSet**定義關聯性端點和關聯性角色。  
  
-   **EntityType**項目會針對 BISM 擴充以提供其他詳細資訊的資料表和欄位，其中包含屬性排序的資料行和顯示用途。  
  
-   **量值**項目會定義模型中可用的計算。 量值可以藉由新增一組特殊顯示屬性，使用新轉換成 KPI **KPI**項目。  
  
-   檢視方塊沒有個別表示法。 資料行和資料表未包含在檢視方塊會出現，但加上旗標與 CSDL 中**隱藏**屬性。  
  
### <a name="entities-entitysets-and-entitytypes"></a>實體、EntitySet 和 EntityType  
 實體資料架構中實體的概念已擴充，可表示資料模型中的資料行和資料表。 下列摘錄顯示的清單**EntitySet**簡單中的項目建立的模型包含只有三個資料表。  
  
```  
<EntityContainer Name="SimpleModel">  
<EntitySet Name="DimCustomer"EntityType="SimpleModel.DimCustomer">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimDate" EntityType="SimpleModel.DimDate">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimGeography" EntityType="SimpleModel.DimGeography">  
     <bi:EntitySet />  
   </EntitySet> />  
  
```  
  
 **EntitySet**不包含資料行或資料表中的資料相關的資訊。 資料行及其屬性的詳細描述是在 EntityType 元素中提供。  
  
 **EntitySet**每個實體 （資料表） 的項目包含一組屬性會定義索引鍵資料行、 資料類型和長度的資料行 null 屬性、 排序行為等等。 例如，下列 CSDL 摘錄描述的是 Customer 資料表中的三個資料行。 第一個資料行是模型在內部使用的特殊隱藏資料行。  
  
```  
<EntityType Name="Customer">  
  <Key>  
     <PropertyRef Name="RowNumber" />  
  </Key>  
    <Property Name="RowNumber" Type="Int64" Nullable="false">  
     <bi:Property Hidden="true" Contents="RowNumber"  
       Stability="RowNumber" />  
    </Property>  
    <Property Name="CustomerKey" Type="Int64" Nullable="false">  
      <bi:Property />  
    </Property>  
     <Property Name="FirstName" Type="String" MaxLength="Max" FixedLength="false">  
       <bi:Property />  
      </Property>  
  
```  
  
 為了限制產生的 CSDLBI 文件大小，出現一次以上的實體中的屬性會指定以參考現有的屬性，讓屬性需要一次針對列出**EntityType**。 用戶端應用程式可以取得屬性的值，藉由尋找**EntityType**符合**OriginEntityType**。  
  
### <a name="relationships"></a>關聯性  
 在 實體資料架構中，關聯性會定義為*關聯*實體之間。  
  
 關聯永遠只有兩端，每一端都指向資料表中的欄位或資料行。 因此，如果關聯性具有不同的端點，兩個資料表之間就可能會存在多個關聯性。 角色名稱會指派給關聯的端點，表示關聯如何用於資料模型的內容。 角色名稱的範例可能是**ShipTo**，當套用至 Orders 資料表中的客戶識別碼相關的客戶識別碼。  
  
 模型的 CSDLBI 表示法也包含關聯的屬性，以決定如何將實體對應到彼此的*多重性*關聯。 多重性會指出位於資料表之間關聯性端點的屬性或資料行是位於關聯性的一端，還是多端。 一對一關聯性沒有個別的值。 CSDLBI 註解支援多重性 0 (表示實體並未與任何項目產生關聯) 或 0..1 (表示一對一關聯性或一對多關聯性)。  
  
 下列範例表示 Date 與 ProductInventory 資料表之間關聯性的 CSDLBI 輸出，其中這兩個資料表都在 DateAlternateKey 資料行上聯結。 請注意，根據預設，名稱**AssociationSet**是關聯性中涉及的資料行的完整的名稱。 不過，當您設計模型時，可以將此行為變更成使用不同的命名格式。  
  
```  
<AssociationSet Name="ProductInventory_Date_DateKey" Association="Model.ProductInventory_Date_DateKey">  
              <End EntitySet="ProductInventory" />  
              <End EntitySet="Date" />  
              <bi:AssociationSet />  
            </AssociationSet>  
  
```  
  
### <a name="visualization-and-navigation-properties"></a>視覺效果和導覽屬性  
 CSDLBI 註解最重要的部分就是在報表層中定義呈現方式的屬性，以及在實體之間導覽關聯性的屬性。 一般而言，當您建立資料模型時，如果用戶端應用程式會指定呈現方式的排序和其他詳細資料，您就會認為控制資料的排序或分組方式或是控制可能的預設值不重要。 不過，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格式模型是針對與 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 報表用戶端整合所設計，而且包含支援在報表設計介面中呈現資料模型內之實體的屬性 (Property) 與屬性 (Attribute)。  
  
 視覺效果的延伸模組包含了一些屬性，可用於指定要搭配數值資料使用的預設彙總、指出文字欄位會指向影像的 URL，或是指定用來排序目前欄位的欄位。  
  
### <a name="name-properties-and-naming-conventions"></a>名稱屬性和命名慣例  
 CSDLBI 結構描述規定每個實體都必須具有唯一名稱以及可當做索引鍵使用的識別碼。 此外，某些實體可以具有用於顯示用途的標題，以及根據實體使用位置而變更的內容名稱。  
  
 **文件**項目會提供讓報表設計師提供的實體，描述有機會，以便協助商務使用者了解資料的意義。 某些實體也允許使用一個或多個**註解**耗用量提供額外的中繼資料，應用程式或用戶端的屬性。  
  
 當您在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工具中產生模型時，針對物件所建立的名稱就會遵循 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的物件命名和名稱唯一性慣例。 不過，因為 CSDLBI 是以實體資料架構 (EDF) 為基礎 (要求名稱遵守 C# 識別碼的慣例)，所以當伺服器建立模型的 CSDLBI 輸出時，伺服器會接受用於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 結構描述內部的名稱，並且自動建立符合 EDF 需求的新物件名稱。 下表描述的是用以產生新名稱的作業。  
  
|規則|動作|  
|----------|------------|  
|沒有禁止的字元|由底線取代禁止的字元。|  
|名稱必須是唯一的|如果兩個字串完全相同，就會附加底線及數字，讓其中一個字串成為唯一的字串|  
  
> [!WARNING]  
>  標題和限定詞都具有翻譯，而且對於給定的語言而言，可能會存在其中一個。 這表示，如果限定詞與名稱或限定詞與標題已串連，則字串可能使用兩種不同的語言。  
  
## <a name="additions-to-support-multidimensional-models"></a>支援多維度模型的新增功能  
 CSDLBI 1.0 版註解僅支援表格式模型。 1.1 版中已加入使用傳統 BI 開發工具所建立之多維度模型 (OLAP Cube) 的支援。 因此，現在您可以對多維度模型發出 XML 要求，並且接收模型的 CSDLBI 定義，以便於報表中使用。  
  
 **Cube:** SQL Server[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]表格式資料庫只能包含一個模式。 相反地，每個多維度資料庫都可包含多個 Cube，且每個資料庫會與預設 Cube 產生關聯。 因此，對多維度伺服器發出 XML 要求時，必須指定 Cube，否則將會傳回預設 Cube 的 XML。  
  
 另外，Cube 的表示法非常類似表格式模型資料庫的表示法。 Cube 名稱和 Cube 會對應表格式資料庫名稱和資料庫識別碼。  
  
 **維度：**維度會以 CSDLBI 表示為實體 （資料表） 的資料行和屬性。 請注意，即使未包含在檢視方塊中，包含在模型中的維度仍將表示在 CSDL 輸出中，標示為**隱藏**。  
  
 **檢視方塊：**用戶端可以要求個別檢視方塊的 CSDL。 如需詳細資訊，請參閱[DISCOVER_CSDL_METADATA 資料列集](../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)。  
  
 **階層：**支援階層，並且以 CSDLBI 表示為一組層級。  
  
 **成員：**的支援已新增的預設成員，預設值會自動加入 CSDLBI 輸出。  
  
 **導出成員：**多維度模型支援導出的成員的子系**所有**含單一真實成員。  
  
 **維度屬性：** CSDLBI 輸出中，維度屬性都支援，而且會自動標記為非彙總。  
  
 **Kpi:** CSDLBI 1.1 版中支援 Kpi，但表示法已變更。 KPI 之前是量值的屬性。 在 1.1 版中，KPI 元素可以加入至量值  
  
 **新屬性：**已加入以支援 DirectQuery 模型的其他屬性。  
  
 **限制：**不支援資料格安全性。  
  
## <a name="see-also"></a>另請參閱  
 [商業智慧的 CSDL 註解 &#40;CSDLBI&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
  

