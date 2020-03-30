---
title: 資料集欄位集合 (報表產生器) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: b3884576-1f7e-4d40-bb7d-168312333bb3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b33041f7debc2ad75268973867c72e073459f1de
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "77077784"
---
# <a name="dataset-fields-collection-report-builder-and-ssrs"></a>資料集欄位集合 (報表產生器及 SSRS)
  資料集欄位代表資料連接中的資料。 欄位可以代表數值或非數值資料。 範例包括銷售量、總銷售額、客戶名稱、資料庫識別碼、URL、影像、空間資料及電子郵件地址。 在設計介面上，欄位會以報表項目 (如文字方塊、資料表和圖表) 中的運算式形式出現。  
  
 報表擁有三種類型的欄位，而且會將其顯示於 [報表資料] 窗格中：資料集欄位、資料集導出欄位和內建欄位。  
  
-   **資料集欄位。** 代表欄位集合的中繼資料，當針對資料來源執行資料集查詢時，將會傳回這些欄位。  
  
-   **資料集導出欄位。** 您針對資料集建立的其他欄位。 每一個導出欄位的建立方式都是藉由評估您所定義的運算式。  
  
-   **內建欄位。** 代表報表產生器所提供之欄位集合的中繼資料，這些欄位會在處理報表時提供報表資訊，例如報表名稱或時間。 如需詳細資訊，請參閱[內建的全域和使用者參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)。  
  
 資料集欄位名稱會當做報表資料集定義的一部分來儲存。 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="dataset-fields-and-queries"></a><a name="Fields"></a> 資料集欄位和查詢  
 資料集欄位是由資料集查詢命令以及您所定義之任何導出欄位所指定。 您在報表中看到的欄位集合取決於您具有的資料集類型：  
  
-   **共用資料集。** 欄位集合是當您直接將共用資料集加入報表，或是當您加入的報表組件已包含共用資料集時，共用資料集定義內查詢的欄位清單。 當報表伺服器上的共用資料集定義變更時，本機欄位集合將不會變更。 若要更新本機欄位集合，您必須重新整理本機共用資料集的清單。  
  
-   **內嵌資料集。** 欄位集合是針對資料來源執行目前的查詢時所傳回的欄位清單。  
  
 如需詳細資訊，請參閱[加入、編輯、重新整理報表資料窗格中的欄位 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
  
### <a name="calculated-fields"></a>導出欄位  
 您可藉由建立運算式來手動指定導出欄位。 導出欄位可用來建立不存在於資料來源上的新值。 例如，導出欄位可代表新值、一組欄位值的自訂排序次序，或是轉換成另一個資料類型的現有欄位。  
  
 導出欄位在報表的本機，而且不能儲存為共用資料集的一部分。  
  
 如需詳細資訊，請參閱[加入、編輯、重新整理報表資料窗格中的欄位 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)。  
  
  
### <a name="entities-and-entity-fields"></a>實體和實體欄位  
 如果您正在處理報表模型資料來源，您可將實體和實體欄位指定為報表資料。 在報表模型的查詢設計工具中，您可以透過互動方式來瀏覽及選取相關實體，並選擇您要併入報表資料集的欄位。 當您完成查詢的設計之後，您可以在 [報表資料] 窗格內查看實體識別碼和實體欄位的集合。 實體識別碼是由報表模型自動產生，通常不會對使用者顯示。  
  
### <a name="using-extended-field-properties"></a>使用擴充欄位屬性  
 支援多維度查詢的資料來源 (例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]) 可支援欄位上欄位屬性。 欄位屬性會出現在查詢的結果集中，但是在 **[報表資料]** 窗格中則看不到。 欄位屬性仍然可供您的報表使用。 若要參考欄位的屬性，請將欄位拖曳到報表上，然後將預設屬性 **Value** 變更為您想要之屬性的欄位名稱。 例如在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cube 中，您可以針對 Cube 資料格中的值來定義格式。 可以使用欄位屬性 **FormattedValue**來取得格式化的值。 若要直接使用該值，而不是使用值並設定文字方塊的格式屬性，請將欄位拖曳到文字方塊，並將預設運算式 `=Fields!FieldName.Value` 變更為 `=Fields!FieldName.FormattedValue`。  
  
> [!NOTE]
>  並非所有 **Field** 屬性都可用於所有資料來源。 **Value** 和 **IsMissing** 屬性是為所有資料來源定義的。 其他預先定義的屬性 (例如多維度資料來源的 **Key**、 **UniqueName**和 **ParentUniqueName** ) 只有在資料來源有提供這些屬性時，才受到支援。 某些資料提供者可支援自訂屬性。 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。 例如，如果是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源，請參閱 [Analysis Services 資料庫的擴充欄位屬性 &#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)。  
  
  
##  <a name="understanding-default-expressions-for-fields"></a><a name="Defaults"></a> 了解欄位的預設運算式  
 文字方塊可以是報表主體中的文字方塊報表項目，或是 Tablix 資料區資料格中的文字方塊。 當您將欄位與文字方塊連結時，文字方塊的位置會決定欄位參考的預設運算式。 在報表主體中，文字方塊值運算式必須指定彙總和資料集。 如果報表中只有一個資料集存在，系統會為您建立這個預設運算式。 如果是代表數值的欄位，預設彙總函式為 Sum。 如果是代表非數值的欄位，預設彙總函式為 First。  
  
 在 Tablix 資料區中，預設欄位運算式取決於您加入欄位之文字方塊的資料列和群組成員資格。 Sales 欄位的欄位運算式 (當加入到資料表之詳細資料列中的文字方塊時) 為 `[Sales]`。 如果您將相同的欄位加入到群組首中的文字方塊，預設運算式就是 `(Sum[Sales])`，因為群組首會顯示群組的摘要值，而非詳細資料值。 當報表執行時，報表處理器會評估每一個運算式，並替代報表中的結果。  
  
 如需運算式的詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)。  
  
  
##  <a name="field-data-types"></a><a name="DataTypes"></a> 欄位資料類型  
 當您建立資料集時，資料來源上欄位的資料類型可能不完全是報表中使用的資料類型。 資料類型可能會經歷一或兩個對應層。 資料處理延伸模組或資料提供者可以將資料來源中的資料類型對應到 Common Language Runtime (CLR) 資料類型。 資料處理延伸模組所傳回的資料類型會從 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]對應到 Common Language Runtime (CLR) 資料類型的子集。  
  
 在資料來源上，資料會使用此資料來源所支援的資料類型來儲存。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料必須是其中一個支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，例如 **nvarchar** 或 **datetime**。 當您從此資料來源擷取資料時，資料會透過與資料來源類型相關聯的資料處理延伸模組或資料提供者來傳遞。 根據資料處理延伸模組而定，資料可從資料來源使用的資料類型轉換成資料處理延伸模組所支援的資料類型。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用與 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]一起安裝之 Common Language Runtime (CLR) 所支援的資料類型。 資料提供者會將結果集中的每一個資料行從原生資料類型對應到 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) 資料類型。  
  
 在每一個階段，資料都是由資料類型來表示，如以下清單所述：  
  
-   **資料來源** ：您所連接之資料來源類型版本所支援的資料類型。  
  
     例如，適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的一般資料類型包括 **int**、 **datetime**和 **varchar**。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 所引進的資料類型新增了 **date**、 **time**、 **datetimetz**和 **datetime2**的支援。 如需詳細資訊，請參閱 [資料類型 (Transact-SQL)](https://go.microsoft.com/fwlink/?linkid=98362)。  
  
-   **資料提供者或資料處理延伸模組** ：當您連接到資料來源時，您所選取之資料處理延伸模組的資料提供者版本所支援的資料類型。 以 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 為基礎的資料提供者會使用 CLR 所支援的資料類型。 如需 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者資料類型的詳細資訊，請參閱 MSDN 上的 [資料類型對應 (ADO.NET)](https://go.microsoft.com/fwlink/?LinkId=112178) 和 [使用基底類型](https://go.microsoft.com/fwlink/?LinkId=112177) 。  
  
     例如， [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 所支援的一般資料類型包括 **Int32** 和 **String**。 **DateTime** 結構支援日曆上的日期和時間。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 Service Pack 1 針對具有時區時差的日期引進了 **DateTimeOffset** 結構的支援。  
  
    > [!NOTE]  
    >  報表伺服器會使用報表伺服器上所安裝及設定的資料提供者。 [預覽] 模式下的報表撰寫用戶端會使用用戶端電腦上所安裝及設定的資料處理延伸模組。 您必須同時在報表用戶端和報表伺服器環境下測試您的報表。  
  
-   **報表處理器** ：資料類型是以您安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]時所安裝的 CLR 版本為基礎。  
  
     例如， [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 已導入報表處理器用於新日期和時間類型的日期類型，如下表所示：  
  
    |SQL 資料類型|CLR 資料類型|描述|  
    |-------------------|-------------------|-----------------|  
    |**日期**|**DateTime**|僅限日期|  
    |**Time**|**TimeSpan**|只有時間|  
    |**DateTimeTZ**|**DateTimeOffset**|包含時區時差的日期和時間|  
    |**DateTime2**|**DateTime**|包含毫秒的日期和時間|  
  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫類型的詳細資訊，請參閱 [資料類型 (Database Engine)](https://go.microsoft.com/fwlink/?linkid=98362) 和 [日期和時間資料類型與函數 (Transact-SQL)](https://go.microsoft.com/fwlink/?linkid=98360)。  
  
 如需從運算式加入資料集欄位之參考的詳細資訊，請參閱[運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)。  
  
  
##  <a name="detecting-missing-fields-at-run-time"></a><a name="MissingFields"></a> 在執行階段偵測遺漏的欄位  
 當報表處理時，資料集的結果集可能不包含指定之所有資料行的值，因為資料行不再存在於資料來源中。 您可以使用欄位屬性 IsMissing 來偵測是否在執行階段傳回欄位的值。 如需詳細資訊，請參閱[資料集 Fields 集合參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-dataset-fields-collection-references-report-builder.md)。  
  
  
## <a name="see-also"></a>另請參閱  
 [資料集屬性對話方塊、欄位 &#40;報表產生器&#41;](https://msdn.microsoft.com/library/75c7e54a-3d20-4c9a-88da-ab36dce2ce42)   
 [報表產生器中的報表組件和資料集](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
