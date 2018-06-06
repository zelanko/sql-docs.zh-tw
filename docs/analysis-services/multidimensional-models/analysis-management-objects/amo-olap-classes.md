---
title: AMO OLAP 類別 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1d457c26a0b2d33058a5eb496825a6dc03dbc71
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="amo-olap-classes"></a>AMO OLAP 類別
  分析管理物件 (AMO) OLAP 類別可協助您建立、修改、刪除和處理 Cube、維度及相關的物件，例如關鍵效能指標 (KPI)、動作和主動式快取。  
  
 如需設定 AMO 程式設計環境，如何與伺服器建立連線，存取資料庫，或是定義資料來源和資料來源檢視，請參閱[AMO 基礎類別](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)。  
  
 本主題包含下列幾節：  
  
-   [維度物件](#Dimensions)  
  
-   [Cube 物件](#Cubes)  
  
-   [MeasureGroup 物件](#MeasureGroups)  
  
-   [分割區物件](#Partition)  
  
-   [AggregationDesign 物件](#AggregationDesign)  
  
-   [Aggregation 物件](#Aggregation)  
  
-   [動作物件](#Action)  
  
-   [KPI 物件](#KPI)  
  
-   [檢視方塊物件](#Perspective)  
  
-   [翻譯物件](#Translation)  
  
-   [ProactiveCaching 物件](#ProactiveCaching)  
  
 下圖顯示在本主題中說明的類別關聯性。  
  
 ![AMO 中的 OLAP 類別](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-olapclasses.gif "AMO 中的 OLAP 類別")  
  
## <a name="basic-classes"></a>基本類別  
  
###  <a name="Dimensions"></a> 維度物件  
 建立維度的方式是將它加入父資料庫的維度集合，並使用 Update 方法將 <xref:Microsoft.AnalysisServices.Dimension> 物件更新到伺服器。  
  
 若要移除維度，必須使用 <xref:Microsoft.AnalysisServices.Dimension> 的 Drop 方法來卸除它。 使用 Remove 方法從資料庫的維度集合移除 <xref:Microsoft.AnalysisServices.Dimension>，並不會將它從伺服器刪除，只會從 AMO 物件模型刪除。  
  
 可以在建立 <xref:Microsoft.AnalysisServices.Dimension> 物件之後處理它。 <xref:Microsoft.AnalysisServices.Dimension> 可以使用自己的處理方法來加以處理，或者可以在父物件處理時，使用父物件的處理方法來處理。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.Dimension>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
###  <a name="Cubes"></a> Cube 物件  
 建立 Cube 的方式是將它加入資料庫的 Cube 集合，然後使用 Update 方法將 <xref:Microsoft.AnalysisServices.Cube> 物件更新到伺服器。 Cube 的 Update 方法可以包括參數 UpdateOptions.ExpandFull，以確保 Cube 中所有修改過的物件，都會因這個更新動作而更新到伺服器。  
  
 若要移除 Cube，必須使用 <xref:Microsoft.AnalysisServices.Cube> 的 Drop 方法來卸除它。 從集合移除 Cube 並不會影響伺服器。  
  
 可以在建立 <xref:Microsoft.AnalysisServices.Cube> 物件之後處理它。 <xref:Microsoft.AnalysisServices.Cube> 可以使用自己的處理方法來加以處理，或者可以在父物件使用自己的 Process 方法處理自己時來處理它。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.Cube>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
###  <a name="MeasureGroups"></a>MeasureGroup 物件  
 建立量值群組的方式是將它加入 Cube 的量值群組集合，然後使用它自己的 Update 方法將 <xref:Microsoft.AnalysisServices.MeasureGroup> 物件更新到伺服器。 可以使用 <xref:Microsoft.AnalysisServices.MeasureGroup> 物件自己的 Drop 方法來移除它。  
  
 可以在建立 <xref:Microsoft.AnalysisServices.MeasureGroup> 物件之後處理它。 <xref:Microsoft.AnalysisServices.MeasureGroup> 可以使用自己的 Process 方法加以處理，或者可以在父物件使用自己的 Process 方法處理自己時來處理它。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.MeasureGroup>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
###  <a name="Partition"></a>分割區物件  
 建立 <xref:Microsoft.AnalysisServices.Partition> 物件的方式是將它加入父量值群組的資料分割集合，然後使用 Update 方法更新伺服器上的 <xref:Microsoft.AnalysisServices.Partition> 物件。 可以使用 Drop 方法來移除 <xref:Microsoft.AnalysisServices.Partition> 物件。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.Partition>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
###  <a name="AggregationDesign"></a>AggregationDesign 物件  
 彙總設計是從 <xref:Microsoft.AnalysisServices.AggregationDesign> 物件使用 AggregationDesign 方法來建構。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.AggregationDesign>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
###  <a name="Aggregation"></a>Aggregation 物件  
 建立 <xref:Microsoft.AnalysisServices.Aggregation> 物件的方式是將它加入父量值群組的彙總設計集合，然後使用 Update 方法更新伺服器上的父量值群組物件。 透過使用 Remove 方法或是 RemoveAt 方法從 <xref:Microsoft.AnalysisServices.AggregationCollection> 移除彙總。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.Aggregation>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
## <a name="advanced-classes"></a>進階類別  
 進階類別提供超越建立和瀏覽 Cube 的 OLAP 功能。 以下是一些進階類別及其提供的優點：  
  
-   動作類別是用以在瀏覽 Cube 的某些區域時，建立主動式回應。  
  
-   關鍵效能指標 (KPI) 允許資料值之間的比較分析。  
  
-   檢視方塊提供單一 Cube 的選取檢視，好讓使用者可以著重在對他們很重要的項目上。  
  
-   翻譯允許將 Cube 自訂成使用者地區設定。  
  
-   主動式快取類別可以在 MOLAP 儲存的增強式效能及 ROLAP 儲存的立即性之間提供平衡，並提供排程的資料分割處理。  
  
 AMO 是用以為此增強的行為設定定義，但是實際的經驗是由實作所有這些增強功能的瀏覽用戶端所定義。  
  
###  <a name="Action"></a>動作物件  
 建立 <xref:Microsoft.AnalysisServices.Action> 物件的方式是將它加入 Cube 的動作集合，然後使用 Update 方法將 <xref:Microsoft.AnalysisServices.Cube> 物件更新到伺服器。 Cube 的更新方法可以包括參數 UpdateOptions.ExpandFull，以確保 Cube 中所有修改過的物件，都會因這個更新動作而更新到伺服器。  
  
 若要移除 <xref:Microsoft.AnalysisServices.Action> 物件，必須將它從集合移除，而且必須更新父 Cube。  
  
 必須先更新及處理 Cube，才可以從用戶端使用動作。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.Action>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
###  <a name="KPI"></a> Kpi 物件  
 建立 <xref:Microsoft.AnalysisServices.Kpi> 物件的方式是將它加入 Cube 的 KPI 集合，然後使用 Update 方法將 <xref:Microsoft.AnalysisServices.Cube> 物件更新到伺服器。 Cube 的 Update 方法可以包括參數 UpdateOptions.ExpandFull，以確保 Cube 中所有修改過的物件，都會隨這個更新動作更新到伺服器。  
  
 若要移除 <xref:Microsoft.AnalysisServices.Kpi> 物件，必須將它從集合移除，然後必須更新父 Cube。  
  
 必須先更新及處理 Cube，才可以使用 KPI。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.Kpi>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
###  <a name="Perspective"></a>檢視方塊物件  
 建立 <xref:Microsoft.AnalysisServices.Perspective> 物件的方式是將它加入 Cube 的檢視方塊集合，然後使用 Update 方法將 <xref:Microsoft.AnalysisServices.Cube> 物件更新到伺服器。 Cube 的 Update 方法可以包括參數 UpdateOptions.ExpandFull，以確保 Cube 中所有修改過的物件，都會隨這個更新動作更新到伺服器。  
  
 若要移除 <xref:Microsoft.AnalysisServices.Perspective> 物件，必須將它從集合移除，然後必須更新父 Cube。  
  
 Cube 必須要先更新及處理，然後才可以使用檢視方塊。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.Perspective>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
###  <a name="Translation"></a>翻譯物件  
 建立 <xref:Microsoft.AnalysisServices.Translation> 物件的方式是將它加入所需物件的翻譯集合，然後使用 Update 方法將最接近的主要父物件更新到伺服器。 最接近的父物件之 Update 方法可以包括參數 UpdateOptions.ExpandFull，以確保已修改的所有子系物件，都會隨這個更新動作更新到伺服器。  
  
 若要移除 <xref:Microsoft.AnalysisServices.Translation> 物件，必須將它從集合移除，然後必須更新最接近的父物件。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.Translation>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
###  <a name="ProactiveCaching"></a>ProactiveCaching 物件  
 建立 <xref:Microsoft.AnalysisServices.ProactiveCaching> 物件的方式是將它加入維度或資料分割的主動式快取物件集合，然後使用 Update 方法將維度或資料分割物件更新到伺服器。  
  
 若要移除 <xref:Microsoft.AnalysisServices.ProactiveCaching> 物件，必須將它從集合移除，然後必須更新父物件。  
  
 必須先更新和處理維度或資料分割，才可以啟用主動式快取，使其準備好可供使用。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.ProactiveCaching>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices>   
 [AMO 類別簡介](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [程式設計 AMO OLAP 基本物件](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-basic-objects.md)   
 [設計 AMO OLAP 進階物件](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-advanced-objects.md)   
 [邏輯架構 & #40;Analysis Services-多維度資料 & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [資料庫物件 & #40;Analysis Services-多維度資料 & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
