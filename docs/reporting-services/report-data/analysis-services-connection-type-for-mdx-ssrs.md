---
title: MDX 的 Analysis Services 連線類型 (SSRS) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: bd2e7148-3124-4e07-9734-22333127c3be
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 44b3755f118bcd3550f34cb617fa3b71e0879e55
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43274286"
---
# <a name="analysis-services-connection-type-for-mdx-ssrs"></a>Analysis Services Connection Type for MDX (SSRS)
  若要在報表中包含來自 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cube 的資料，您必須擁有以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]類型的報表資料來源為基礎的資料集。 此內建資料來源類型是以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料延伸模組為基礎。 您可以從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cube 擷取有關維度、階層、層級、關鍵效能指標 (KPI)、量值和屬性的中繼資料，用來做為報表資料。  
  
 此資料處理延伸模組支援多值參數、伺服器彙總，以及與連接字串分開管理的認證。  
  
 您可以使用本主題中的資訊來建置資料來源。 如需逐步指示，請參閱 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 連接字串  
 當您連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cube 時，會連接到伺服器上 Analysis Services 執行個體中的資料庫物件。 資料庫可能有多個 Cube。 您會在建立查詢時，指定在查詢設計工具中的 Cube。 下列範例顯示連接字串：  
  
```  
data source=<server name>;initial catalog=<database name>  
```  
  
 如需更多連接字串範例，請參閱 [報表產生器中的資料連接、資料來源及連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)。  
  
  
##  <a name="Credentials"></a> 認證  
 需要有認證才能夠執行報表、於本機預覽報表並且從報表伺服器預覽報表。  
  
 發行報表之後，您可能需要變更資料來源的認證，如此當報表在報表伺服器上執行時，擷取資料的權限就會是有效的。  
  
 報表撰寫用戶端提供下列可用來指定認證的選項：  
  
-   目前的 Windows 使用者 (也稱為整合式安全性)。  
  
-   使用預存的使用者名稱和密碼。  
  
-   提示使用者提供認證。 此選項只支援 Windows 整合式安全性。  
  
-   不需要認證。 若要使用這個選項，您先前必須在報表伺服器上設定自動執行帳戶。 如需詳細資訊，請參閱 msdn.microsoft.com 上 [Reporting Services 文件](http://go.microsoft.com/fwlink/?linkid=121312)中的[設定自動執行帳戶 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
 如需詳細資訊，請參閱[資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 或[在報表產生器中指定認證](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
  
##  <a name="Query"></a> 查詢  
 擁有與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源的資料連接之後，您會建立資料集並定義多維度運算式 (MDX) 查詢，用來指定要從 Cube 擷取的資料。 使用 MDX 圖形化查詢設計工具瀏覽，並且從資料來源的基礎資料結構進行選取。  
  
 您可以利用下列方式指定查詢：  
  
-   以互動方式建立查詢。 Analysis Services MDX 查詢設計工具支援下列檢視：  
  
    -   **設計檢視** ：將維度、成員、成員屬性、量值和 KPI 從中繼資料瀏覽器拖曳到 **[資料]** 窗格，以建立 MDX 查詢。 請將導出成員從 [導出成員] 窗格拖曳到 [資料] 窗格，以便建立其他資料集欄位。  
  
    -   **查詢檢視** ：將維度、成員、成員屬性、量值和 KPI 從中繼資料瀏覽器拖曳到 [查詢] 窗格，以建立 MDX 查詢。 您可以在 [查詢] 窗格中直接編輯 MDX 文字。 請將導出成員從 [導出成員] 窗格拖曳到 [查詢] 窗格，以便定義其他資料集欄位。  
  
     如需詳細資訊，請參閱 [Analysis Services MDX 查詢設計工具使用者介面 &#40;報表產生器&#41;](http://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26)。  
  
-   從報表匯入現有的 MDX 查詢。 請使用 **[匯入查詢]** 按鈕來瀏覽到 .rdl 檔案，然後匯入查詢。 您可以從包含以 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源為基礎之內嵌資料集的報表匯入查詢。 不支援直接從 .mdx 檔案匯入 MDX 查詢。  
  
 在執行階段中，執行查詢以檢視結果集。 查詢結果會自動擷取成扁平化的資料列集。 查詢結果集中的資料行會填入資料集的欄位集合。 在您建立查詢之後，請在 [報表資料] 窗格中檢視從中繼資料產生的資料集欄位集合。 當報表執行時，實際資枓會從外部資料來源傳回。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料處理延伸模組支援擴充資料集欄位屬性。 這些值可從外部資料來源取得，但是不會出現在 [報表資料] 窗格中。 您可以透過內建的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Fields **集合，在報表中使用** 資料處理延伸模組支援的擴充欄位屬性。 至於資料來源上具有值的屬性，您可以存取預先定義的屬性值，例如 **FormattedValue**、 **Color**或 **UniqueName**。 如需詳細資訊，請參閱 msdn.microsoft.com 上 [Analysis Services 資料庫的擴充欄位屬性 &#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)。  
  
  
##  <a name="Parameters"></a> 參數  
 若要包含查詢參數，請在查詢設計工具的篩選區域中建立篩選，然後再將該篩選標示成參數。 系統會針對每一個篩選自動建立一個資料集，以提供可用的值。 根據預設，這些資料集不會出現在 [報表資料] 窗格內。 如需詳細資訊，請參閱[在 Analysis Services 的 MDX 查詢設計工具中定義參數 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md) 和[針對多維度資料的參數值顯示隱藏的資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/show-hidden-datasets-for-parameter-values-multidimensional-data.md)。  
  
 根據預設，每個報表參數都具有 **[文字]** 資料類型。 建立報表參數後，您可能必須變更預設值。 如需詳細資訊，請參閱 MSDN 上的 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)類型之報表資料來源為基礎的資料集。  
  
  
##  <a name="Remarks"></a> 備註  
 Analysis Services 資料延伸模組是以 XMLA (XML for Analysis) 通訊協定為基礎。 Cube 的結果集是透過 XMLA 通訊協定擷取成扁平化的資料列集。 不支援不完全階層。 如需詳細資訊，請參閱 [不完全階層](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md)。  
  
 您也可以從 OLE DB 資料來源類型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cube 擷取資料。 如需詳細資訊，請參閱 [OLE DB 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)。  
  
 如需版本支援的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ 線上叢書](http://go.microsoft.com/fwlink/?linkid=121312)》中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
  
##  <a name="Related"></a> 相關章節  
 本文件集的這些章節會提供報表資料的深入概念性資訊，以及如何定義、自訂和使用與報表資料相關組件的程序資訊。  
  
 [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 提供存取報表資料的概觀。  
  
 [報表產生器中的資料連接、資料來源及連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 提供資料連接與資料來源的相關資訊。  
  
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供內嵌與共用資料集的相關資訊。  
  
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 提供查詢所產生之資料集欄位集合的相關資訊。  
  
 [Analysis Services 資料庫的擴充欄位屬性 &#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)  
 提供有關可透過 XMLA 資料提供者提供之額外欄位的資訊。  
  
 《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書》](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
 提供支援每一個資料延伸模組之平台與版本的深入資訊。  
  
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
