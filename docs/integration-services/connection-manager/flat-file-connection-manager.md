---
title: 一般檔案連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ffileconnection.general.f1
- sql13.dts.designer.ffileconnection.columns.f1
- sql13.dts.designer.ffileconnection.columnproperties.f1
- sql13.dts.designer.ffileconnection.preview.f1
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2cf3156597035241398e354e8c80bfebb9c16d67
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728275"
---
# <a name="flat-file-connection-manager"></a>一般檔案連接管理員

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  「一般檔案」連接管理員可讓封裝存取一般檔案中的資料。 例如，「一般檔案」來源與目的地可以使用「一般檔案」連接管理員來擷取並載入資料。  
  
 「一般檔案」連接管理員僅可存取一個檔案。 若要參考多個檔案，請使用「多個一般檔案」連接管理員，而非「一般檔案」連接管理員。 如需詳細資訊，請參閱 [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)。  
  
## <a name="column-length"></a>資料行長度  
 依預設，「一般檔案」連接管理員會將字串資料行的長度設定成 50 個字元。 在 [一般檔案連接管理員編輯器]  對話方塊中，您可以評估取樣資料，並自動調整這些資料行的長度，以避免資料遭截斷或超出資料行寬度。 此外，除非接著在一般檔案來源或轉換中調整資料行長度，否則字串資料行在整個資料流程中的資料行長度將維持不變。 如果這些字串資料行對應到較窄的目的地資料行，使用者介面中將會出現警告。 此外，執行階段中也可能發生因為資料截斷所產生的錯誤。 若要避免錯誤或資料截斷，您可以調整資料行的大小，使其與一般檔案連接管理員、一般檔案來源或轉換中的目的地資料行相容。 若要修改輸出資料行的長度，您可以在 **[進階編輯器]** 對話方塊的 **[輸入與輸出屬性]** 索引標籤中設定輸出資料行的 **Length** 屬性。  
  
 如果在加入及設定使用「一般檔案」連接管理員的一般檔案來源之後，在該連接管理員中更新資料行長度，您就不需要手動調整一般檔案來源中輸出資料行的大小。 在您開啟 **[一般檔案來源]** 對話方塊時，一般檔案來源會提供一個用來同步化資料行中繼資料的選項。  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>設定一般檔案連接管理員  
 當您將「一般檔案」連接管理員加入封裝時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立連接管理員 (在執行階段解析為「一般檔案」連接)、設定「一般檔案」連接屬性，並將「一般檔案」連接管理員加入封裝的 **Connections** 集合。  
  
 連接管理員的 **ConnectionManagerType** 屬性會設為 [FLATFILE] 。  
  
 根據預設，「一般檔案」連接管理員一律會檢查未加引號之資料中的資料列分隔符號，並在找到資料列分隔符號時開始一個新資料列。 這可讓連接管理員正確地剖析資料列缺少資料行欄位的檔案。  
  
 在某些情況下，停用此功能可能會提升封裝效能。 您可以將「一般檔案」連接管理員屬性 **AlwaysCheckForRowDelimiters**設定為 [False] ，以停用此功能。  
  
 您可以利用下列方式設定「一般檔案」連接管理員：  
  
-   指定要使用的檔案、地區設定及字碼頁。 地區設定用於解譯區分地區設定的資料 (如日期)，字碼頁用於將字串資料轉換為 Unicode。  
  
-   指定檔案格式。 您可以使用分隔的、固定寬度或不齊右格式。  
  
-   指定標頭資料列、資料列和資料行分隔符號。 資料行分隔符號可以在檔案層級設定，並在資料行層級覆寫。  
  
-   指示檔案中的第一個資料列是否包含資料行名稱。  
  
-   指定文字限定詞字元。 每個資料行都可以設定為識別文字限定詞。  
  
     一般檔案連線管理員支援使用限定詞字元，將限定詞字元內嵌到限定字串中。 文字限定詞的雙執行個體會解譯成常值 (該字串的單一執行個體)。 例如，文字限定詞如果是單引號，而輸入資料為 'abc'、'def'、'g'hi'，則輸出資料為 abc、def、g'hi。 不過，內嵌在限定字串中的限定詞執行個體，會造成一般檔案來源因錯誤 DTS_E_PRIMEOUTPUTFAILED 而失敗。
  
-   在個別的資料行上設定屬性，例如名稱、資料類型和最大寬度。  
  
 您可以針對一般檔案連接管理員來設定 ConnectionString 屬性，其方式是在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 [屬性] 視窗中指定運算式。 為避免驗證錯誤，請執行下列操作。  
  
-   當您使用運算式指定檔案時，請在 [一般檔案連接管理員編輯器]  的 [檔案名稱] 方塊中加入檔案路徑。  
  
-   在「一般檔案」連接管理員上將 **DelayValidation** 屬性設定為 [True] 。  
  
 您可以透過具有「一般檔案」目的地的「一般檔案」連接管理員，使用運算式在執行階段建立檔案名稱。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="flat-file-connection-manager-editor-general-page"></a>一般檔案連接管理員編輯器 (一般頁面)
  使用 **[一般檔案連接管理員編輯器]** 對話方塊的 **[一般]** 頁面，來選取檔案和資料格式。 一般檔案連接可以讓封裝連接到文字檔。  
  
 若要深入了解一般檔案連接管理員，請參閱＜ [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)＞。  
  
### <a name="options"></a>選項。  
 **連線管理員名稱**  
 提供唯一的名稱給工作流程中的一般檔案連接。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連接。 最佳作法是以其用途描述連接，使封裝可以自我記錄並易於維護。  
  
 **檔案名稱**  
 輸入在一般檔案連接中要使用的路徑和檔案名稱。  
  
 **瀏覽**  
 尋找在一般檔案連接中要使用的檔案名稱。  
  
 **地區設定**  
 指定地區設定以提供排序以及日期和時間格式的特定語言資訊。  
  
 **Unicode**  
 指出是否使用 Unicode。 如果使用 Unicode，您就無法指定字碼頁。  
  
 **字碼頁**  
 指定非 Unicode 文字的字碼頁。  
  
 **格式**  
 指出檔案是要使用分隔符號、固定寬度或不齊右的格式。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|使用分隔符號|資料行是以分隔符號隔開，分隔符號是在 **[資料行]** 頁面上指定的。|  
|固定寬度|資料行具有固定寬度。|  
|不齊右|不齊右檔案就是除了最後一個資料行之外，其他所有資料行都有固定寬度的檔案。 它是以資料列分隔符號分隔。|  
  
 **文字定位項**  
 指定要使用的文字限定詞。 例如，您可以指定文字欄位加上引號。  
  
> [!NOTE]  
>  選取文字限定詞之後，就無法重新選取 [無] 選項。 輸入 **None** 即可取消選取文字限定詞。  
  
 **標頭資料列分隔符號**  
 從標頭資料列的分隔符號清單中選取，或輸入分隔符號文字。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|標頭資料列是以歸位字元和換行字元的組合分隔。|  
|**{CR}**|標頭資料列是以歸位字元分隔。|  
|**{LF}**|標頭資料列是以換行字元分隔。|  
|**分號 {;}**|標頭資料列是以分號分隔。|  
|**冒號 {:}**|標頭資料列是以冒號分隔。|  
|**逗號 {,}**|標頭資料列是以逗號分隔。|  
|**定位字元 {t}**|標頭資料列是以定位字元分隔。|  
|**分隔號 {&#124;}**|標頭資料列是以分隔號 (&#124;) 分隔。|  
  
 **略過的標頭資料列數**  
 指定要略過的標頭資料列數或初始資料列數 (如果有的話)。  
  
 **第一個資料列的資料行名稱**  
 指出在第一個資料列中，是否為資料行名稱或需要提供資料行名稱。  
## <a name="flat-file-connection-manager-editor-columns-page"></a>一般檔案連接管理員編輯器 (資料行頁面)
  使用 **[一般檔案連接管理員編輯器]** 對話方塊的 **[資料行]** 頁面來指定資料列和資料行資訊，以及預覽檔案。  
  
 若要深入了解一般檔案連接管理員，請參閱＜ [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)＞。  
  
### <a name="static-options"></a>靜態選項  
 **連線管理員名稱**  
 提供唯一的名稱給工作流程中的一般檔案連接。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連接。 最佳作法是以其用途描述連接，使封裝可以自我記錄並易於維護。  
  
### <a name="flat-file-format-dynamic-options"></a>一般檔案格式動態選項  
  
#### <a name="format--delimited"></a>格式 = 使用分隔符號  
 **資料列分隔符號**  
 從可用的資料列分隔符號清單中選取，或輸入分隔符號文字。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|資料列是以歸位字元和換行字元的組合分隔。|  
|**{CR}**|資料列是以歸位字元分隔。|  
|**{LF}**|資料列是以換行字元分隔。|  
|**分號 {;}**|資料列是以分號分隔。|  
|**冒號 {:}**|資料列是以冒號分隔。|  
|**逗號 {,}**|資料列是以逗號分隔。|  
|**定位字元 {t}**|資料列是以定位字元分隔。|  
|**分隔號 {&#124;}**|資料列是以分隔號分隔。|  
  
 **資料行分隔符號**  
 從可用的資料行分隔符號清單中選取，或輸入分隔符號文字。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|資料行是以歸位字元和換行字元的組合分隔。|  
|**{CR}**|資料行是以歸位字元分隔。|  
|**{LF}**|資料行是以換行字元分隔。|  
|**分號 {;}**|資料行是以分號分隔。|  
|**冒號 {:}**|資料行是以冒號分隔。|  
|**逗號 {,}**|資料行是以逗號分隔。|  
|**定位字元 {t}**|資料行是以定位字元分隔。|  
|**分隔號 {&#124;}**|資料行是以分隔號分隔。|  
  
 **[重新整理]**  
 按一下 [重新整理]，即可檢視變更要略過之分隔符號的影響。 僅在您已變更其他連接選項之後，才會看見此按鈕。  
  
 **預覽資料列**  
 檢視一般檔案中的範例資料，使用選取的選項將資料分為資料行和資料列。  
  
 **重設資料行**  
 按一下 [重設資料行]，即可將原始資料行以外的資料行全部移除。  
  
#### <a name="format--fixed-width"></a>格式 = 固定寬度  
 **字型**  
 選取要顯示預覽資料的字型。  
  
 **來源資料行**  
 滑動垂直紅色資料列標記，即可調整資料列的寬度；而按一下預覽視窗上方的尺規，即可調整資料行的寬度  
  
 **資料列寬度**  
 為個別資料行加入分隔符號之前，請先指定資料列的長度。 或者，在預覽視窗中拖曳垂直紅線來標示資料列結尾。 資料列寬度值會自動更新。  
  
 **重設資料行**  
 按一下 [重設資料行]，即可將原始資料行以外的資料行全部移除。  
  
#### <a name="format--ragged-right"></a>格式 = 不齊右  
  
> [!NOTE]  
>  不齊右檔案就是除了最後一個資料行之外，其他所有資料行都有固定寬度的檔案。 它是以資料列分隔符號分隔。  
  
 **字型**  
 選取要顯示預覽資料的字型。  
  
 **來源資料行**  
 滑動垂直紅色資料列標記，即可調整資料列的寬度；而按一下預覽視窗上方的尺規，即可調整資料行的寬度  
  
 **資料列分隔符號**  
 從可用的資料列分隔符號清單中選取，或輸入分隔符號文字。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|資料列是以歸位字元和換行字元的組合分隔。|  
|**{CR}**|資料列是以歸位字元分隔。|  
|**{LF}**|資料列是以換行字元分隔。|  
|**分號 {;}**|資料列是以分號分隔。|  
|**冒號 {:}**|資料列是以冒號分隔。|  
|**逗號 {,}**|資料列是以逗號分隔。|  
|**定位字元 {t}**|資料列是以定位字元分隔。|  
|**分隔號 {&#124;}**|資料列是以分隔號分隔。|  
  
 **重設資料行**  
 按一下 [重設資料行]，即可將原始資料行以外的資料行全部移除。  
## <a name="flat-file-connection-manager-editor-advanced-page"></a>一般檔案連接管理員編輯器 (進階頁面)
  您可以使用 [一般檔案連線管理員編輯器] 對話方塊的 [進階] 頁面設定屬性，以指定 Integration Services 讀取及寫入一般檔案的方式。 您可以變更一般檔案中的資料行名稱，並設定屬性以包含檔案中每個資料行的資料類型和分隔符號。  
  
 字串資料行的長度預設為 50 個字元。 您可以調整這些資料行的長度，以避免截斷資料或資料行寬度過大。 您也可更新其他中繼資料，以啟用與目的地資料行的相容性。 例如，您可能會將只包含整數資料之資料行的資料類型變更成數值資料類型 (例如 DT_I2)。 您可以手動進行這些修改，也可以按一下 [選取類型] 按鈕，使用 [建議資料行類型] 對話方塊評估範例資料，並自動為您進行其中某些變更。  
  
 若要深入了解一般檔案連接管理員，請參閱＜ [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)＞。  
  
### <a name="options"></a>選項。  
 **連接管理員名稱**  
 提供唯一的名稱給工作流程中的一般檔案連接管理員。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連接管理員。 最佳作法是以其用途描述連接管理員，使封裝可以自我記錄並易於維護。  
  
 **設定每一個資料行的屬性**  
 請在左窗格中選取一個資料行以便在右窗格中檢視它的屬性。 請參閱下表以了解資料類型屬性的描述。 部分列出的屬性，只能在某些一般檔案格式中設定。  
  
|屬性|Description|  
|--------------|-----------------|  
|**ColumnType**|代表資料行是否為分隔的、固定寬度或不齊右。 此屬性是唯讀的。 不齊右檔案就是除了最後一個資料行之外，其他所有資料行都有固定寬度的檔案。 它是以資料列分隔符號分隔。|  
|**OutputColumnWidth**|指定儲存為位元組計數的值；針對 Unicode 檔案，此值將對應至字元計數。 在資料流程工作中，這個值將用來替一般檔案來源設定輸出資料行寬度。 在物件模型中，這個屬性的名稱為 MaximumWidth。|  
|**DataType**|從可用的資料類型清單中選取。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。|  
|**TextQualified**|指出文字資料是否會由文字限定詞字元 (例如引號字元) 括住。<br /><br /> True：一般檔案中文字資料是限定的。 False：一般檔案中的文字資料是「非」限定的。|  
|**名稱**|提供描述性資料行名稱。 如果未輸入名稱， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會自動以 Column 0、Column 1 等等的格式建立名稱。|  
|**DataScale**|指定數值資料的小數位數。 小數位數是指小數位數的數目。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。|  
|**ColumnDelimiter**|從可用的資料行分隔符號清單中選取。 請選擇不太可能會在文字中出現的分隔符號。 固定寬度資料行將忽略這個值。<br /><br /> **{CR}{LF}** ： 資料行是以歸位字元和換行字元的組合分隔。<br /><br /> **{CR}** ： 資料行是以歸位字元分隔。<br /><br /> **{LF}** ： 資料行是以換行字元分隔。<br /><br /> **分號 {;}** ： 資料行是以分號分隔。<br /><br /> **冒號 {:}** ： 資料行是以冒號分隔。<br /><br /> **逗號 {,}** . 資料行是以逗號分隔。<br /><br /> **定位字元 {t}** ： 資料行是以定位字元分隔。<br /><br /> **分隔號 {&#124;}** ： 資料行是以分隔號分隔。|  
|**DataPrecision**|指定數值資料的有效位數。 有效位數是指位數的數目。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。|  
|**InputColumnWidth**|指定將儲存為位元組計數的值；針對 Unicode 檔案，這將會顯示為字元計數。 分隔資料行將忽略這個值。<br /><br /> **注意** ︰在物件模型中，這個屬性的名稱為 ColumnWidth。|  
  
 **新增**  
 按一下 [新增] 來加入新的資料行。 依預設，[新增] 按鈕會在清單結尾加入新的資料行。 此按鈕還有下列選項，可以在下拉式清單中使用。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**加入資料行**|在清單結尾加入新資料行。|  
|**插在前面**|在選取的資料行之前插入新資料行。|  
|**插在後面**|在選取的資料行之後插入新資料行。|  
  
 **刪除**  
 選取資料行，然後按一下 [刪除] 將其移除。  
  
 **建議類型**  
 使用 [建議資料行類型] 對話方塊，評估檔案中的範例資料，並取得對每個資料行之資料類型和長度的建議。 如需詳細資訊，請參閱 [建議資料行類型對話方塊 UI 參考](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md)。  
## <a name="flat-file-connection-manager-editor-preview-page"></a>一般檔案連接管理員編輯器 (預覽頁面)
  使用 [一般檔案連線管理員編輯器] 對話方塊的 [預覽] 節點，即可以表格式格式來檢視來源檔案的內容。  
  
 若要深入了解一般檔案連接管理員，請參閱＜ [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)＞。  
  
### <a name="options"></a>選項。  
 **連線管理員名稱**  
 提供唯一的名稱給工作流程中的一般檔案連接。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連接。 最佳作法是以其用途描述連接，使封裝可以自我記錄並易於維護。  
  
 **略過的資料列數**  
 指定在一般檔案開頭要略過的資料列數。  
  
 **[重新整理]**  
 按一下 [重新整理]，即可檢視變更要略過之資料列數的影響。 僅在您已變更其他連接選項之後，才會看見此按鈕。  
  
 **預覽資料列**  
 檢視一般檔案中的範例資料，根據您選取的選項將資料分為資料行和資料列。  
 
