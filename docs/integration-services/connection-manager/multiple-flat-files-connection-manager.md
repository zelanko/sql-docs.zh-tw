---
title: 多個一般檔案連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.multifile.advanced.f1
- sql13.dts.designer.multifile.columns.f1
- sql13.dts.designer.multifile.general.f1
- sql13.dts.designer.multifile.preview.f1
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c93f0be480341abb59038db34616a94d4b475952
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298510"
---
# <a name="multiple-flat-files-connection-manager"></a>多個一般檔案連接管理員

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  「多個一般檔案」連接管理員可讓封裝存取多個一般檔案中的資料。 例如，當資料流程工作位於迴圈容器 (如 For 迴圈容器) 內時，「一般檔案」來源可以使用「多個一般檔案」連接管理員。 在此容器的每一個迴圈上，「一般檔案」來源會從「多個一般檔案」連接管理員提供的下一個檔案名稱中載入資料。  
  
 當您將「多個一般檔案」連線管理員新增至套件時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立一個連線管理員 (在執行階段會解析為「多個一般檔案」連線)、設定「多個一般檔案」連線管理員的屬性，並將「多個一般檔案」連線管理員新增至套件的 **Connections** 集合。  
  
 連接管理員的 **ConnectionManagerType** 屬性會設為 **MULTIFLATFILE**。  
  
 您可以利用下列方式設定「多個一般檔案」連接管理員：  
  
-   指定要使用的檔案、地區設定和字碼頁。 地區設定用於解譯區分地區設定的資料 (如日期)，字碼頁用於將字串資料轉換為 Unicode。  
  
-   指定檔案格式。 您可以使用分隔的、固定寬度或不齊右格式。  
  
-   指定標頭資料列、資料列和資料行分隔符號。 資料行分隔符號可以在檔案層級設定，並在資料行層級覆寫。  
  
-   指出檔案中的第一個資料列是否包含資料行名稱。  
  
-   指定文字限定詞字元。 每個資料行都可以設定為識別文字限定詞。  
  
-   在個別的資料行上設定屬性，例如名稱、資料類型和最大寬度。  
  
 如果「多個一般檔案」連接管理員參考多個檔案，則檔案的路徑會以垂直線 (|) 字元隔開。 連接管理員的 **ConnectionString** 屬性具有下列格式：  
  
 \<*path*>|\<*path*>  
  
 您也可以使用萬用字元來指定多個檔案。 例如，若要參考 C 磁碟機上的所有文字檔， **ConnectionString** 屬性的值可以設定為 C:\\\*.txt。  
  
 如果「多個一般檔案」連接管理員參考多個檔案，則所有檔案必須具有相同的格式。  
  
 依預設，「多個一般檔案」連接管理員會將字串資料行的長度設定成 50 個字元。 在 **[多個一般檔案連接管理員編輯器]** 對話方塊中，您可以評估取樣資料，並自動調整這些資料行的長度，以避免資料遭截斷或超出資料行寬度。 除非在一般檔案來源或轉換中調整資料行長度，否則在整個資料流程中，資料行長度將維持不變。 如果這些資料行對應到較窄的目的資料行，使用者介面中將會出現警告，而且在執行階段中可能發生因為資料截斷所產生的錯誤。 您可以調整資料行的大小，使其與一般檔案連接管理員、一般檔案來源或轉換中的目的地資料行相容。 若要修改輸出資料行的長度，您可以在 **[進階編輯器]** 對話方塊的 **[輸入與輸出屬性]** 索引標籤中設定輸出資料行的 **Length** 屬性。  
  
 如果在加入及設定使用「多個一般檔案」連接管理員的一般檔案來源之後，在該連接管理員中更新資料行長度，您就不需要手動調整一般檔案來源中輸出資料行的大小。 在您開啟 **[一般檔案來源]** 對話方塊時，一般檔案來源會提供一個用來同步化資料行中繼資料的選項。  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>設定多個一般檔案連接管理員  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="multiple-flat-files-connection-manager-editor-general-page"></a>多個一般檔案連線管理員編輯器 (一般頁面)
  使用 **[多個一般檔案連線管理員編輯器]** 對話方塊的 **[一般]** 頁面，即可選取一組具有相同資料格式的檔案，並指定其資料格式。 多個一般檔案連接，可以讓封裝連接到一組具有相同格式的文字檔。  
  
 若要深入了解多個一般檔案連接管理員，請參閱＜ [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)＞。  
  
### <a name="options"></a>選項。  
 **連線管理員名稱**  
 提供唯一的名稱給工作流程中的多個一般檔案連接。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連接。 最佳作法是以其用途描述連接，使封裝可以自我記錄並易於維護。  
  
 **檔案名稱**  
 輸入路徑和檔案名稱，以便於多個一般檔案連接中使用。 您可以使用萬用字元來指定多個檔案，例如 "C:\\*.txt"，或者使用分隔號 (|) 來分隔多個檔案名稱。 所有檔案必須有相同的資料格式。  
  
 **瀏覽**  
 瀏覽檔案名稱，以便於多個一般檔案連接中使用。 您可以選取多個檔案。 所有檔案必須有相同的資料格式。  
  
 **地區設定**  
 指定地區，以提供排序以及時間和日期的轉換資訊。  
  
 **Unicode**  
 指出是否使用 Unicode。 使用 Unicode 即無需指定字碼頁。  
  
 **字碼頁**  
 指定非 Unicode 文字的字碼頁。  
  
 **格式**  
 指出是要使用分隔符號、固定寬度或不齊右的格式。 所有檔案必須有相同的資料格式。  
  
|值|描述|  
|-----------|-----------------|  
|Delimited (分隔檔)|資料行是以分隔符號隔開，分隔符號是在 **[資料行]** 頁面上指定的。|  
|固定寬度|資料行具有固定寬度，由 **[資料行]** 頁面上的拖曳標記線所指定。|  
|不齊右|不齊右檔案就是除了最後一個資料行是由資料列分隔符號所分隔之外，其他所有資料行都有在 **[資料行]** 頁面上所指定之固定寬度的檔案。|  
  
 **文字定位項**  
 指定要使用的文字限定詞。 例如，您可以指定文字必須加上引號。  
  
 **標頭資料列分隔符號**  
 從標頭資料列的分隔符號清單中選取，或輸入分隔符號文字。  
  
|值|描述|  
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
 指定要略過的標頭列數 (如果有的話)。  
  
 **第一個資料列的資料行名稱**  
 指出在第一個資料列中，是否為資料行名稱或需要提供資料行名稱。  
  
## <a name="multiple-flat-files-connection-manager-editor-columns-page"></a>多個一般檔案連接管理員編輯器 (資料行頁面)
  使用 **[多個一般檔案連接管理員編輯器]** 對話方塊的 **[資料行]** 節點，來指定資料列與資料行資訊以及預覽第一個選取的檔案。  
  
 若要深入了解多個一般檔案連接管理員，請參閱＜ [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)＞。  
  
### <a name="static-options"></a>靜態選項  
 **連線管理員名稱**  
 提供唯一的名稱給工作流程中的多個一般檔案連接。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連接。 最佳作法是以其用途描述連接，使封裝可以自我記錄並易於維護。  
  
### <a name="flat-file-format-dynamic-options"></a>一般檔案格式動態選項  
  
#### <a name="format--delimited"></a>格式 = 使用分隔符號  
 **資料列分隔符號**  
 從可用的資料列分隔符號清單中選取，或輸入分隔符號文字。  
  
|值|描述|  
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
  
|值|描述|  
|-----------|-----------------|  
|**{CR}{LF}**|資料行是以歸位字元和換行字元的組合分隔。|  
|**{CR}**|資料行是以歸位字元分隔。|  
|**{LF}**|資料行是以換行字元分隔。|  
|**分號 {;}**|資料行是以分號分隔。|  
|**冒號 {:}**|資料行是以冒號分隔。|  
|**逗號 {,}**|資料行是以逗號分隔。|  
|**定位字元 {t}**|資料行是以定位字元分隔。|  
|**分隔號 {&#124;}**|資料行是以分隔號分隔。|  
  
 **重設資料行**  
 按一下 [重設資料行]  ，即可將原始資料行以外的資料行全部移除。  
  
#### <a name="format--fixed-width"></a>格式 = 固定寬度  
 **字型**  
 選取要顯示預覽資料的字型。  
  
 **來源資料行**  
 滑動垂直資料列標記，即可調整資料列的寬度，而按一下預覽視窗上方的尺規，即可調整資料行的寬度  
  
 **資料列寬度**  
 為個別資料行加入分隔符號之前，請先指定資料列的長度。 或者，在預覽視窗中拖曳垂直線來標示資料列結尾。 資料列寬度值會自動更新。  
  
 **重設資料行**  
 按一下 [重設資料行]  ，即可將原始資料行以外的資料行全部移除。  
  
#### <a name="format--ragged-right"></a>格式 = 不齊右  
  
> [!NOTE]  
>  不齊右檔案是除了最後一個資料行以外，每一個資料行都有固定寬度。 它是以資料列分隔符號分隔。  
  
 **字型**  
 選取要顯示預覽資料的字型。  
  
 **來源資料行**  
 滑動垂直資料列標記，即可調整資料列的寬度，而按一下預覽視窗上方的尺規，即可調整資料行的寬度  
  
 **資料列分隔符號**  
 從可用的資料列分隔符號清單中選取，或輸入分隔符號文字。  
  
|值|描述|  
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
 按一下 [重設資料行]  ，即可將原始資料行以外的資料行全部移除。  
  
## <a name="multiple-flat-files-connection-manager-editor-advanced-page"></a>多個一般檔案連接管理員編輯器 (進階頁面)
  使用 [多個一般檔案連線管理員編輯器]  對話方塊的 [進階]  頁面，來設定各種屬性，例如一般檔案連線管理員所連接的文字檔中，每個資料行的資料類型和分隔符號。  
  
 字串資料行的長度預設為 50 個字元。 您可以評估範例資料，並自動重新調整這些資料行的長度，以避免截斷資料或資料行寬度過大。 您也可更新其他中繼資料，以啟用與目的地資料行的相容性。 例如，您可能會將只包含整數資料之資料行的資料類型變更成數值資料類型 (例如 DT_I2)。  
  
 若要深入了解多個一般檔案連接管理員，請參閱＜ [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)＞。  
  
### <a name="options"></a>選項。  
 **連線管理員名稱**  
 提供唯一的名稱給工作流程中的多個一般檔案連接管理員。 提供的名稱將顯示在  **設計師的 [連線管理員]** [!INCLUDE[ssIS](../../includes/ssis-md.md)] 區域內。  
  
 **說明**  
 描述連接管理員。 最佳作法是以其用途描述連接管理員，使封裝可以自我記錄並易於維護。  
  
 **設定每一個資料行的屬性**  
 請在左窗格中選取一個資料行以便在右窗格中檢視它的屬性。 請參閱下表以了解資料類型屬性的描述。 部分列出的屬性，只能在某些一般檔案格式中設定。  
  
|屬性|描述|  
|--------------|-----------------|  
|**ColumnType**|代表資料行是否為分隔的、固定寬度或不齊右。 這個屬性是唯讀的。 不齊右檔案就是除了最後一個資料行是由資料列分隔符號所終止之外，其他所有資料行都有固定寬度的檔案。|  
|**OutputColumnWidth**|指定將儲存為位元組計數的值；針對 Unicode 檔案，這將會顯示為字元計數。 在資料流程工作中，這個值將用來替一般檔案來源設定輸出資料行寬度。<br /><br /> 注意：在物件模型中，這個屬性的名稱為 MaximumWidth。|  
|**DataType**|從可用的資料類型清單中選取。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。|  
|**TextQualified**|使用文字限定詞字元指出文字資料是否為限定的：<br /><br /> **True**：一般檔案中的文字資料是限定的。<br /><br /> **False**：一般檔案中的文字資料是非限定的。|  
|**名稱**|提供資料行名稱。 預設為已編號的資料行清單；然而，您可以選擇任何唯一的、描述性的名稱。|  
|**DataScale**|指定數值資料的小數位數。 小數位數是指小數位數的數目。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。|  
|**ColumnDelimiter**|從可用的資料行分隔符號清單中選取。 請選擇不太可能會在文字中出現的分隔符號。 固定寬度資料行將忽略這個值。<br /><br /> **{CR}{LF}** ：資料行是以歸位字元和換行字元的組合分隔<br /><br /> **{CR}** ：資料行是以歸位字元分隔<br /><br /> **{LF}** ：資料行是以換行字元分隔<br /><br /> **分號 {;}** ：資料行是以分號分隔<br /><br /> **冒號 {:}** ：資料行是以冒號分隔<br /><br /> **逗號{,}** ：資料行是以逗號分隔<br /><br /> **定位字元 {t}** ：資料行是以定位字元分隔<br /><br /> **分隔號 {&#124;}** ：資料行是以分隔號分隔|  
|**DataPrecision**|指定數值資料的有效位數。 有效位數是指位數的數目。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。|  
|**InputColumnWidth**|指定將儲存為位元組計數的值；針對 Unicode 檔案，這將會顯示為字元計數。 分隔資料行將忽略這個值。<br /><br /> **注意** ︰在物件模型中，這個屬性的名稱為 ColumnWidth。|  
  
 **新增**  
 按一下 [新增]  來加入新的資料行。 [新增]  按鈕預設會在清單結尾加入新資料行。 此按鈕還有下列選項，可以在下拉式清單中使用。  
  
|值|描述|  
|-----------|-----------------|  
|**加入資料行**|在清單結尾加入新資料行。|  
|**插在前面**|在選取的資料行之前插入新資料行。|  
|**插在後面**|在選取的資料行之後插入新資料行。|  
  
 **刪除**  
 選取資料行，然後按一下 [刪除]  將其移除。  
  
 **建議類型**  
 使用 [建議資料行類型]  對話方塊，可評估第一個選定檔案中的範例資料，並取得對每個資料行之資料類型和長度的建議。 如需詳細資訊，請參閱 [建議資料行類型對話方塊 UI 參考](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md)。  
  
## <a name="multiple-flat-files-connection-manager-editor-preview-page"></a>多個一般檔案連接管理員編輯器 (預覽頁面)
  使用 [多個一般檔案連線管理員編輯器]  對話方塊的 [預覽]  頁面，即可根據您定義的資料行分隔，來檢視第一個所選取來源檔的內容。  
  
 若要深入了解多個一般檔案連接管理員，請參閱＜ [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)＞。  
  
### <a name="options"></a>選項。  
 **連線管理員名稱**  
 提供唯一的名稱給工作流程中的多個一般檔案連接。 提供的名稱將顯示在  **設計師的 [連線管理員]** [!INCLUDE[ssIS](../../includes/ssis-md.md)] 區域內。  
  
 **說明**  
 描述連接。 最佳作法是以其用途描述連接，使封裝可以自我記錄並易於維護。  
  
 **略過的資料列數**  
 指定在一般檔案開頭要略過的資料列數。  
  
 **預覽資料列**  
 檢視第一個選取的一般檔案中的範例資料，使用選取的選項將資料分為資料行和資料列。  
  
## <a name="see-also"></a>另請參閱  
 [一般檔案來源](../../integration-services/data-flow/flat-file-source.md)   
 [一般檔案目的地](../../integration-services/data-flow/flat-file-destination.md)   
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
