---
title: 連線至一般檔案資料來源 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d7e7067b-f5a5-482f-b97e-9d82fe8e9f76
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e1c2789d8d10928bcbe576fc57f630675fdbd405
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65723896"
---
# <a name="connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard"></a>連線至一般檔案資料來源 (SQL Server 匯入和匯出精靈)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本主題示範如何透過 [SQL Server 匯入和匯出精靈] 的 [選擇資料來源] 或 [選擇目的地] 頁面，連線至**一般檔案** (文字檔) 資料來源。 針對一般檔案，精靈的這兩個頁面會呈現不同的選項集，因此，本主題會分別描述一般檔案來源和一般檔案目的地。

## <a name="an-alternative-for-simple-text-import"></a>簡單文字匯入的替代方式
如果您需要將文字檔匯入至 SQL Server，但不需要使用 [匯入和匯出精靈] 中的所有設定選項，則請考慮使用 SQL Server Management Studio (SSMS) 中的 [匯入一般檔案精靈]。 如需詳細資訊，請參閱下列文章：
- [What's new in SQL Server Management Studio 17.3](https://blogs.technet.microsoft.com/dataplatforminsider/2017/10/10/whats-new-in-sql-server-management-studio-17-3/) (SQL Server Management Studio 17.3 的新功能)
- [在 SSMS 17.3 中新推出的「匯入一般檔案精靈」簡介](https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173) \(英文\)

## <a name="connect-to-a-flat-file-source"></a>連線至一般檔案來源
 
 有四個頁面的選項可供一般檔案資料來源使用。 頁面很多！ 但您不需要在每個頁面上花很多時間。 以下是要考慮的工作。
 
頁面|建議  |類型  
----|---------|---------
**一般**|請確定更新 [格式] 區段中的選項。|建議    
**資料行**|請確定您檢查資料行和資料列分隔符號 (適用於分隔符號檔案) 或標示資料行 (適用於固定寬度檔案)。|建議
**進階**|選擇性地檢查資料類型以及預設指派給資料行的其他屬性。|選擇性
**預覽**|選擇性地使用您指定的設定來預覽資料範例。|選擇性

## <a name="general-page-source"></a>一般頁面 (來源)
 在 [一般] 頁面上，瀏覽並選取檔案，然後確認 [格式] 區段中的設定。
 
 ![一般檔案連接一般](../../integration-services/import-export-data/media/flat-file-connection-general.png)  

### <a name="options-to-specify-general-page"></a>要指定的選項 ([一般] 頁面)

 **檔案名稱**  
 輸入一般檔案的路徑和檔案名稱。  
  
 **瀏覽**  
 找到一般檔案。  
  
 **地區設定**  
 指定地區設定，以提供排序以及日期和時間格式的語言特定資訊。  
  
 **Unicode**  
 指定檔案是否使用 Unicode。 如果使用 Unicode，就無法指定字碼頁。  
  
 **字碼頁**  
 指定非 Unicode 文字的字碼頁。  
  
 **格式**  
 選取檔案是要使用分隔符號、固定寬度還是不齊右格式。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|使用分隔符號|資料行是以分隔符號分隔。 您可以在 [資料行] 頁面上指定分隔符號。|  
|固定寬度|資料行具有固定寬度。|  
|不齊右|不齊右檔案就是除了最後一個資料行是由資料列分隔符號所分隔之外，其他所有資料行都有固定寬度的檔案。|  
  
 **文字定位項**  
 指定檔案所使用的文字限定詞 (如果有的話)。 例如，您可以指定文字欄位加上引號。 (此屬性只適用於分隔符號檔案)。 
  
> [!NOTE]
> 選取文字限定詞之後，就無法重新選取 [無] 選項。 輸入 **None** 即可取消選取文字限定詞。  
  
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
 如果有的話，請在檔案頂端指定要略過的資料列數目。  
  
 **第一個資料列的資料行名稱**  
 指定第一個資料列 (在任何跳過的資料列之後) 是否包含資料行名稱。

## <a name="columns-page---format--delimited-source"></a>資料行頁面 - 格式 = 使用分隔符號 (來源)
 在 [資料行] 頁面上，確認精靈已識別的資料行和分隔符號清單。 下列螢幕擷取畫面顯示將 [分隔符號] 選取為一般檔案格式時的頁面。
 
![一般檔案、分隔符號、資料行頁面](../../integration-services/import-export-data/media/flat-file-delimited-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--delimited"></a>要指定的選項 ([資料行] 頁面 - 格式 = 使用分隔符號)

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
  
 **預覽資料列**  
 檢視一般檔案中的範例資料，使用選取的選項將資料分為資料行和資料列。  
 
 **[重新整理]**  
 按一下 [重新整理]，即可檢視變更要略過之分隔符號的影響。 僅在您已變更其他連接選項之後，才會看見此按鈕。  
  
 **重設資料行**  
 還原原始資料行。  

## <a name="columns-page---format--fixed-width-source"></a>資料行頁面 - 格式 = 固定寬度 (來源)
在 [資料行] 頁面上，確認精靈已識別的資料行和分隔符號清單。 下列螢幕擷取畫面顯示將 [固定寬度] 選取為一般檔案格式時的頁面。
  
![一般檔案、固定寬度、資料行頁面](../../integration-services/import-export-data/media/flat-file-fixed-width-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--fixed-width"></a>要指定的選項 ([資料行] 頁面 - 格式 = 固定寬度)

 **字型**  
 選取要顯示預覽資料的字型。  
  
 **來源資料行**  
 滑動垂直紅色資料列標記，即可調整資料列的寬度；而按一下預覽視窗上方的尺規，即可調整資料行的寬度  
  
 **資料列寬度**  
 為個別資料行加入分隔符號之前，請先指定資料列的長度。 或者，在預覽視窗中拖曳垂直紅線來標示資料列結尾。 資料列寬度值會自動更新。  
  
 **重設資料行**  
 還原原始資料行。  
  
## <a name="columns-page---format--ragged-right-source"></a>資料行頁面 - 格式 = 不齊右 (來源)
在 [資料行] 頁面上，確認精靈已識別的資料行和分隔符號清單。 下列螢幕擷取畫面顯示將 [不齊右] 選取為一般檔案格式時的頁面。

> [!NOTE]
> 不齊右檔案就是除了最後一個資料行是由資料列分隔符號所分隔之外，其他所有資料行都有固定寬度的檔案。  
 
![一般檔案、不齊右、資料行頁面](../../integration-services/import-export-data/media/flat-file-ragged-right-columns-page.jpg)

### <a name="options-to-specify-columns-page---format--ragged-right"></a>要指定的選項 ([資料行] 頁面 - 格式 = 不齊右)
   
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
 還原原始資料行。  

## <a name="advanced-page-source"></a>進階頁面 (來源)
[進階] 頁面會顯示資料來源中每個資料行的詳細資訊，包括其資料類型和大小。 下列螢幕擷取畫面顯示分隔符號一般檔案中第一個資料行的 [進階] 頁面。

![一般檔案、分隔符號、進階頁面](../../integration-services/import-export-data/media/flat-file-delimited-advanced-page.jpg)

在螢幕擷取畫面中，請注意包含數字的 [識別碼] 資料行一開始會有字串資料類型。

### <a name="options-to-specify-advanced-page"></a>要指定的選項 ([進階] 頁面)

 **設定每一個資料行的屬性**  
 請在左窗格中選取一個資料行以便在右窗格中檢視它的屬性。 請參閱下表以了解資料行屬性的描述。 列出的部分屬性只能針對特定一般檔案格式以及特定資料類型的資料行進行設定。  
  
|屬性|Description|  
|--------------|-----------------|  
|**名稱**|提供描述性資料行名稱。 如果您未輸入名稱，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會自動以 Column 0、Column 1 等等的格式建立名稱。|
|**ColumnDelimiter**|從可用的資料行分隔符號清單中選取。 請選擇不太可能會在文字中出現的分隔符號。 固定寬度資料行將忽略這個值。<br /><br /> **{CR}{LF}**： 資料行是以歸位字元和換行字元的組合分隔。<br /><br /> **{CR}**： 資料行是以歸位字元分隔。<br /><br /> **{LF}**： 資料行是以換行字元分隔。<br /><br /> **分號 {;}**： 資料行是以分號分隔。<br /><br /> **冒號 {:}**： 資料行是以冒號分隔。<br /><br /> **逗號 {,}**. 資料行是以逗號分隔。<br /><br /> **定位字元 {t}**： 資料行是以定位字元分隔。<br /><br /> **分隔號 {&#124;}**： 資料行是以分隔號分隔。|
|**ColumnType**|代表資料行是否為分隔的、固定寬度或不齊右。 此屬性是唯讀的。 不齊右檔案就是除了最後一個資料行之外，其他所有資料行都有固定寬度的檔案。 它是以資料列分隔符號分隔。|  
|**InputColumnWidth**|指定儲存為位元組計數的值；針對 Unicode 檔案，此值是字元計數。 分隔資料行將忽略這個值。<br /><br /> **注意** ︰在物件模型中，這個屬性的名稱為 ColumnWidth。|
|**DataPrecision**|指定數值資料的有效位數。 有效位數是指位數的數目。|
|**DataScale**|指定數值資料的小數位數。 小數位數是指小數位數的數目。|
|**DataType**|從可用的資料類型清單中選取。<br/>如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。|
|**OutputColumnWidth**|指定儲存為位元組計數的值；針對 Unicode 檔案，此值將對應至字元計數。 在資料流程工作中，這個值將用來替一般檔案來源設定輸出資料行寬度。 在物件模型中，這個屬性的名稱為 MaximumWidth。|  
|**TextQualified**|指出文字資料是否會由文字限定詞字元 (例如引號字元) 括住。<br /><br /> True：一般檔案中文字資料是限定的。 False：一般檔案中的文字資料是「非」限定的。|  
  
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
 使用 [建議資料行類型] 對話方塊，評估檔案中的範例資料，並取得對每個資料行之資料類型和長度的建議。  
 
按一下 [建議類型] 以顯示 [建議資料行類型] 對話方塊。 

![一般檔案連線建議類型對話方塊](../../integration-services/import-export-data/media/flat-file-connection-suggest.png)

在 [建議資料行類型] 對話方塊中選擇選項並按一下 [確定] 之後，精靈可能會變更部分資料行的資料類型。

下列螢幕擷取畫面顯示，在您按一下 [建議類型] 之後精靈已辨識出資料來源中的 [識別碼] 資料行實際上是數字而不是文字字串，並且已將資料行的資料類型從字串變更為整數。

![一般檔案連接 (進階後)](../../integration-services/import-export-data/media/flat-file-connection-advanced-after.png)

如需詳細資訊，請參閱[建議資料行類型對話方塊 UI 參考](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md)。

## <a name="preview-page-source"></a>預覽頁面 (來源)

在 [預覽] 頁面上，確認資料行和範例資料的清單是否如您預期的一樣。

![一般檔案、預覽頁面](../../integration-services/import-export-data/media/flat-file-preview-page.jpg)

### <a name="options-to-specify-preview-page"></a>要指定的選項 ([預覽] 頁面)

 **略過的資料列數**  
 指定在一般檔案開頭要略過的資料列數。  
  
 **預覽資料列**  
 檢視一般檔案中的範例資料，根據您選取的選項將資料分為資料行和資料列。
 
 **[重新整理]**  
 按一下 [重新整理]，即可檢視變更要略過之資料列數的影響。 僅在您已變更其他連接選項之後，才會看見此按鈕。  
 
如需 [預覽] 頁面的詳細資訊，請參閱下列 Integration Services 參考頁面 - [一般檔案連接管理員編輯器 &#40;預覽頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)。

## <a name="connect-to-a-flat-file-destination"></a>連線至一般檔案目的地
一般檔案目的地只會有單頁的選項，如下列螢幕擷取畫面所示。 瀏覽並選取檔案，然後確認 [格式] 區段中的設定。

![連線至一般檔案目的地](../../integration-services/import-export-data/media/connect-to-flat-file-destination.jpg)

### <a name="options-to-specify-choose-a-destination-page"></a>要指定的選項 ([選擇目的地] 頁面)

 **檔案名稱**  
 輸入一般檔案的路徑和檔案名稱。  
  
 **瀏覽**  
 找到一般檔案。  
  
 **地區設定**  
 指定地區設定，以提供排序以及日期和時間格式的語言特定資訊。  
  
 **Unicode**  
 指定檔案是否使用 Unicode。 如果使用 Unicode，就無法指定字碼頁。  
  
 **字碼頁**  
 指定非 Unicode 文字的字碼頁。  
  
 **格式**  
 選取檔案是要使用分隔符號、固定寬度還是不齊右格式。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|使用分隔符號|資料行是以分隔符號分隔。 您可以在 [資料行] 頁面上指定分隔符號。|  
|固定寬度|資料行具有固定寬度。|  
|不齊右|不齊右檔案就是除了最後一個資料行是由資料列分隔符號所分隔之外，其他所有資料行都有固定寬度的檔案。|  
  
 **文字定位項**  
 指定檔案所使用的文字限定詞 (如果有的話)。 例如，您可以指定文字欄位加上引號。 (此屬性只適用於分隔符號檔案)。 
  
> [!NOTE] 
> 選取文字限定詞之後，就無法重新選取 [無] 選項。 輸入 **None** 即可取消選取文字限定詞。  

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

