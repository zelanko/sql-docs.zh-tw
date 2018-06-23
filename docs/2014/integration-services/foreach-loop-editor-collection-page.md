---
title: Foreach 迴圈編輯器 （集合頁面） |Microsoft 文件
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.collection.f1
ms.assetid: 95a19dde-61ca-4d9b-aa3d-131fa4264296
caps.latest.revision: 62
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 50ab22c5b36390645aa8f6fb961531479e592188
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135009"
---
# <a name="foreach-loop-editor-collection-page"></a>Foreach 迴圈編輯器 (集合頁面)
  使用 [Foreach 迴圈編輯器] 對話方塊的 [集合] 頁面，即可指定列舉值類型和設定列舉值。  
  
 若要了解 Foreach 迴圈容器以及如何設定該容器，請參閱 [Foreach 迴圈容器](control-flow/foreach-loop-container.md)和[設定 Foreach 迴圈容器](../../2014/integration-services/configure-a-foreach-loop-container.md)。  
  
## <a name="static-options"></a>靜態選項  
 **列舉值**  
 從清單中選取列舉值類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**Foreach 檔案列舉值**|列舉檔案。 選取這個值就會在 **[Foreach 檔案列舉值]** 區段中顯示動態選項。|  
|**Foreach 項目列舉值**|列舉項目中的值。 選取這個值就會在 **[Foreach 項目列舉值]** 區段中顯示動態選項。|  
|**Foreach ADO 列舉值**|列舉資料表或資料表中的資料列。 選取這個值就會在 **[Foreach ADO 列舉值]** 區段中顯示動態選項。|  
|**Foreach ADO.NET 結構描述資料列集列舉值**|列舉結構描述。 選取這個值就會在 **[Foreach ADO.NET 列舉值]** 區段中顯示動態選項。|  
|**Foreach From Variable 列舉值**|列舉變數中的值。 選取這個值就會在 **[Foreach From Variable 列舉值]** 區段中顯示動態選項。|  
|**Foreach NodeList 列舉值**|以 XML 文件列舉節點。 選取這個值就會在 **[Foreach NodeList 列舉值]** 區段中顯示動態選項。|  
|**Foreach SMO 列舉值**|列舉 SMO 物件。 選取這個值就會在 **[Foreach SMO 列舉值]** 區段中顯示動態選項。|  
|**Foreach Azure Blob 列舉值**|列舉指定 Blob 位置中的 Blob 檔案。 選取此值可在 **[Foreach ADO 列舉值]** 區段中顯示動態選項。|  
|**Foreach ADLS 檔案列舉值**|列舉 ADLS 上具有篩選條件的檔案。 選取這個值就會在 [Foreach ADLS 檔案列舉值] 區段中顯示動態選項。|
  
 **運算式**  
 按一下或展開 **[運算式]** ，即可檢視現有屬性運算式的清單。 按一下省略符號 **(...)** 按鈕以加入列舉值屬性的屬性運算式，或是編輯和評估現有的屬性運算式。  
  
 **相關主題**︰[Integration Services &#40;SSIS&#41; 運算式](expressions/integration-services-ssis-expressions.md)、[屬性運算式編輯器](expressions/property-expressions-editor.md)、[運算式產生器](expressions/expression-builder.md)  
  
## <a name="enumerator-dynamic-options"></a>列舉值動態選項  
  
### <a name="enumerator--foreach-file-enumerator"></a>列舉值 = Foreach 檔案列舉值  
 Foreach 檔案列舉值可用來列舉資料夾中的檔案。 例如，如果 Foreach 迴圈包括「執行 SQL」工作，則您可使用 Foreach 檔案列舉值來列舉檔案，而這些檔案包含執行「執行 SQL」工作的 SQL 陳述式。 您也可以將列舉值設定成包括子資料夾。  
  
 因為迴圈中的外部處理序或工作在迴圈執行時加入、重新命名或刪除檔案，所以 Foreach 檔案列舉值所列舉的資料夾和子資料夾內容在迴圈執行時可能會變更。 這表示可能會發生一些非預期的狀況：  
  
-   如果是刪除檔案，則 Foreach 迴圈中的其中一個工作可能會針對與後續工作所用之檔案不同的一組檔案執行工作。  
  
-   如果是重新命名檔案，且外部處理序自動加入檔案以取代重新命名的檔案，則 Foreach 迴圈可能會針對相同的檔案內容執行兩次工作。  
  
-   如果是加入檔案，則可能會很難判斷 Foreach 迴圈執行的是哪個檔案的工作。  
  
 **資料夾**  
 提供要列舉的根資料夾之路徑。  
  
 **瀏覽**  
 瀏覽以尋找根資料夾。  
  
 **檔案**  
 指定要列舉的檔案。  
  
> [!NOTE]  
>  使用萬用字元 (*) 即可指定要包含在集合中的檔案。 例如，若要包括名稱內含 "abc" 的檔案，可使用下列篩選： \*abc\*。  
>   
>  當您指定副檔名時，此列舉值也會傳回附加其他字元之相同副檔名的檔案 (這個行為與作業系統中 **dir** 命令的行為相同，而且此命令也會針對回溯相容性比較 8.3 檔案名稱)。列舉值的這個行為可能會導致非預期的結果。 例如，您只想要列舉 Excel 2003 檔案，而且指定了 "*.xls"。 不過，此列舉值也會傳回 Excel 2007 檔案，因為這些檔案的副檔名為 ".xlsx"。  
>   
>  您可以使用運算式指定要包括在集合內的檔案，方法是展開 [集合] 頁面上的 [運算式]，選取 **FileSpec** 屬性，然後按一下省略符號按鈕 (…) 加入屬性運算式。 如需動態選取所指定檔案的詳細資訊，請參閱 [SSIS - 動態設定檔案遮罩：檔案規格](http://go.microsoft.com/fwlink/?LinkId=238154)  
  
 **完整**  
 選取即可擷取檔案名稱的完整路徑。 如果在檔案選項中指定萬用字元，則會傳回符合篩選的完整路徑。  
  
 **只有名稱**  
 選取即可只擷取檔案名稱。 如果在檔案選項中指定萬用字元，則會傳回符合篩選的檔案名稱。  
  
 **名稱和副檔名**  
 選取即可擷取檔案名稱及其副檔名。 如果在檔案選項中指定萬用字元，則會傳回符合篩選的檔案名稱和副檔名。  
  
 **周遊子資料夾**  
 選取即可在列舉中包含子資料夾。  
  
### <a name="enumerator--foreach-item-enumerator"></a>列舉值 = Foreach 項目列舉值  
 Foreach 項目列舉值可用來列舉集合中的項目。 您指定資料行和資料行值，即可定義集合中的項目。 一個資料列中的所有資料行都可定義項目。 例如，指定用來執行「執行處理」工作之可執行檔及該工作所使用之工作目錄的項目會有兩個資料行，一個會列出可執行檔名稱，而另一個會列出工作目錄。 資料列數目會決定迴圈的重複次數。 如果資料表有 10 個資料列，則迴圈會重複 10 次。  
  
 若要更新執行處理工作的屬性，則使用資料行的索引，您可以將變數對應至項目資料行。 列舉值項目中所定義之第一個資料行的索引值為 0，第二個資料行則為 1，以此類推。 每次重複迴圈時，都會更新變數值。 然後，會透過使用這些變數的屬性運算式來更新「執行處理」工作的 `Executable` 和 `WorkingDirectory` 屬性。  
  
 **定義 For Each 項目集合中的項目**  
 提供資料表中每個資料行的值。  
  
> [!NOTE]  
>  在資料列資料行輸入值之後，就會在資料表中自動加入新的資料列。  
  
> [!NOTE]  
>  如果提供的值與資料行資料類型不相容，文字就會以紅色顯示。  
  
 **資料行資料類型**  
 列出使用中資料行的資料類型。  
  
 **移除**  
 選取項目，然後按一下 **[移除]** 即可從清單中移除。  
  
 **資料行**  
 按一下即可在項目中設定資料行的資料類型。  
  
 **相關主題** [For Each 項目資料行對話方塊 UI 參考](../../2014/integration-services/for-each-item-columns-dialog-box-ui-reference.md)  
  
### <a name="enumerator--foreach-ado-enumerator"></a>列舉值 = Foreach ADO 列舉值  
 Foreach ADO 列舉值可用來列舉 ADO 或 ADO.NET 物件中的資料列或資料表，而這類物件是儲存在變數中。 例如，如果 Foreach 迴圈包括將資料集寫入變數的指令碼工作，您可以使用 Foreach ADO 列舉值來列舉該資料集中的資料列。 如果變數包含 ADO.NET 資料集，則可將列舉值設定成列舉多個資料表中的資料列，或設定成列舉資料表。  
  
 **ADO 物件來源變數**  
 在清單中選取使用者定義變數，或按一下 [\<新增變數...>]，以建立新的變數。  
  
> [!NOTE]  
>  變數必須為物件資料類型，否則會發生錯誤。  
  
 **相關主題**︰[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[加入變數](../../2014/integration-services/add-variable.md)  
  
 **第一個資料表的資料列**  
 選取此選項即可只列舉第一個資料表的資料列。  
  
 **所有資料表的資料列 (僅 ADO.NET 資料集)**  
 選取即可列舉所有資料表的資料列。 唯有所有列舉的物件都是相同 ADO.NET 資料集的成員時，才可以使用此選項。  
  
 **所有資料表 (僅 ADO.NET 資料集)**  
 選取即可只列舉資料表。  
  
### <a name="enumerator--foreach-adonet-schema-rowset-enumerator"></a>列舉值 = Foreach ADO.NET 結構描述資料列集列舉值  
 Foreach ADO.NET 結構描述資料列集列舉值可用來列舉所指定之資料來源的結構描述。 例如，如果 Foreach 迴圈包括「執行 SQL」工作，您可以使用 Foreach ADO.NET 結構描述資料列集列舉值來列舉結構描述 (例如 **AdventureWorks** 資料庫中的資料行)，以及使用「執行 SQL」工作來取得結構描述權限。  
  
 **[連接]**  
 在清單中選 ADO.NET 連線管理員，或按一下 [\<新增連線...>]，以建立新的 ADO.NET 連線管理員。  
  
> [!IMPORTANT]  
>  ADO.NET 連接管理員必須使用 OLE DB 的 .NET 提供者。 如果連接到 SQL Server，則建議使用的提供者是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client，會列在 **[連接管理員]** 對話方塊的 **[OleDb 的 .Net 提供者]** 區段中。  
  
 **相關主題** [ADO Connection Manager](connection-manager/ado-connection-manager.md)、 [Configure ADO.NET Connection Manager](configure-ado-net-connection-manager.md)  
  
 **結構描述**  
 選取要列舉的結構描述。  
  
 **設定限制**  
 設定要套用至指定之結構描述的限制。  
  
 **相關主題** [結構描述限制對話方塊](../../2014/integration-services/schema-restrictions-dialog-box.md)  
  
### <a name="enumerator--foreach-from-variable-enumerator"></a>列舉值 = Foreach From Variable 列舉值  
 Foreach From Variable 列舉值可用來列舉所指定之變數中可列舉的物件。 例如，如果 Foreach 迴圈包括執行查詢並將結果儲存在變數中的「執行 SQL」工作，您可以使用 Foreach From Variable 列舉值來列舉查詢結果。  
  
 **變數**  
 在清單中選取變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**︰[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[加入變數](../../2014/integration-services/add-variable.md)  
  
### <a name="enumerator--foreach-nodelist-enumerator"></a>列舉值 = Foreach NodeList 列舉值  
 Foreach Nodelist 列舉值可用來列舉因為將 XPath 運算式套用至 XML 檔案而產生的 XML 節點集合。 例如，如果 Foreach 迴圈包括指令碼工作，則您可使用 Foreach NodeList 列舉值將符合 XPath 運算式條件的值從 XML 檔案傳送給該指令碼工作。  
  
 套用至 XML 檔案的 XPath 運算式就是儲存在 OuterXPathString 屬性中的外部 XPath 作業。 如果 XPath 列舉型別設定為`ElementCollection`，Foreach NodeList 列舉值可套用儲存在 InnerXPathString 屬性中的項目集合的內部 XPath 運算式。  
  
 若要深入了解 XML 文件和資料，請參閱 MSDN Library 中的[在 .NET Framework 內採用 XML](http://go.microsoft.com/fwlink/?LinkId=56214)。  
  
 **DocumentSourceType**  
 選取 XML 文件的來源類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 XML 文件的來源。|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **DocumentSource**  
 如果 [DocumentSourceType] 設定為 [直接輸入]，請提供 XML 程式碼，或按一下省略符號 (...) 按鈕，以使用 [文件來源編輯器] 對話方塊來提供 XML。  
  
 如果 [DocumentSourceType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>]，以建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [DocumentSourceType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>]，以建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[加入變數](../../2014/integration-services/add-variable.md)。  
  
 **EnumerationType**  
 從清單中選取列舉類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**Navigator**|使用 XPathNavigator 列舉。|  
|**節點**|列舉 XPath 作業傳回的節點。|  
|**NodeText**|列舉 XPath 作業傳回的文字節點。|  
|`ElementCollection`|列舉 XPath 作業傳回的元素節點。|  
  
 **OuterXPathStringSourceType**  
 選取 XPath 字串的來源類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 XML 文件的來源。|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 `OuterXPathString`  
 如果 [OuterXPathStringSourceType] 設定為 [直接輸入]，請提供 XPath 字串。  
  
 如果 [OuterXPathStringSourceType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>]，以建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [OuterXPathStringSourceType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>]，以建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[加入變數](../../2014/integration-services/add-variable.md)。  
  
 **InnerElementType**  
 如果**EnumerationType**設`ElementCollection`，清單中選取內部元素的類型。  
  
 **InnerXPathStringSourceType**  
 選取內部 XPath 字串的來源類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 XML 文件的來源。|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 `InnerXPathString`  
 如果 [InnerXPathStringSourceType] 設定為 [直接輸入]，請提供 XPath 字串。  
  
 如果 [InnerXPathStringSourceType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>]，以建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [InnerXPathStringSourceType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>]，以建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[加入變數](../../2014/integration-services/add-variable.md)。  
  
### <a name="enumerator--foreach-smo-enumerator"></a>列舉值 = Foreach SMO 列舉值  
 Foreach SMO 列舉值可用來列舉 SQL Server 管理物件 (SMO) 物件。 例如，如果 Foreach 迴圈包括「執行 SQL」工作，您可以使用 Foreach SMO 列舉值來列舉 **AdventureWorks** 資料庫中的資料表，並執行用來計算每個資料表中資料列數目的查詢。  
  
 **[連接]**  
 選取現有的 ADO.NET 連線管理員，或按一下 [\<新增連線...>]，以建立新的連線管理員。  
  
 [ADO.NET Connection Manager](connection-manager/ado-net-connection-manager.md), [Configure ADO.NET Connection Manager](configure-ado-net-connection-manager.md)＞  
  
 **列舉**  
 指定要列舉的 SMO 物件。  
  
 **瀏覽**  
 選取 SMO 列舉。  
  
 **相關主題**：[選取 SMO 列舉對話方塊](../../2014/integration-services/select-smo-enumeration-dialog-box.md)  
  
### <a name="enumerator--foreach-azure-blob-enumerator"></a>列舉值 = Foreach Azure Blob 的列舉值  
 **Azure Blob 的列舉值**可讓 SSIS 封裝列舉指定 Blob 位置中的 Blob 檔案。 列舉之 Blob 檔案的名稱可以儲存在變數中，也可以用於 Foreach 迴圈容器中的工作中。  
  
 **Azure 儲存體連線管理員**  
 選取現有的 Azure 儲存體連接管理員，或建立參考 Azure 儲存體帳戶的新連接管理員。  
  
 相關主題：[Azure 儲存體連線管理員](connection-manager/azure-storage-connection-manager.md)。  
  
 **Blob 容器名稱**  
 指定包含要列舉之 Blob 檔案的 Blob 容器之名稱。  
  
 **Blob 目錄**  
 指定指定包含要列舉之 Blob 檔案的 Blob 目錄。 Blob 目錄是虛擬的階層式結構。  
  
 **Blob 名稱篩選**  
 指定名稱篩選條件以列舉具有特定名稱模式的檔案。 例如 MySheet*.xls\* 會包含 MySheet001.xls 及 MySheetABC.xlsx 一類的檔案。  
  
 **Blob 的起迄時間範圍篩選**  
 指定時間範圍篩選條件。 這會列舉在 **TimeRangeFrom** 之後及在 **TimeRangeTo** 之前修改的檔案。  
### <a name="enumerator--foreach-adls-file-enumerator"></a>列舉值 = Foreach ADLS 檔案列舉值  
**ADLS 檔案列舉值**可讓 SSIS 封裝列舉 ADLS 上具有篩選條件的檔案。 斜線 (`/`)-帶有前置詞的完整路徑的列舉檔案可以儲存在變數中，並用於 Foreach 迴圈容器中的工作。
  
**AzureDataLakeConnection**  
指定 Azure Data Lake 連線管理員，或建立參考 ADLS 帳戶的新連線管理員。   
  
**AzureDataLakeDirectory**  
指定要搜尋的 ADLS 目錄。
  
**FileNamePattern**  
指定檔案名稱篩選。 會列舉其名稱符合指定的模式的檔案。 支援萬用字元 `*` 和 `?`。 
  
**SearchRecursively**  
指定是否在指定的目錄內以遞迴方式搜尋。  
  
## <a name="external-resources"></a>外部資源  
  
-   bidn.com 上的部落格文章： [SSIS ForEach NodeList 列舉值](http://go.microsoft.com/fwlink/?LinkId=220671)。  
  
-   beyondrelational.com 上的部落格文章： [SSIS - 動態設定檔案遮罩：FileSpec](http://go.microsoft.com/fwlink/?LinkId=238154)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Foreach 迴圈編輯器&#40;[一般] 頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [Foreach 迴圈編輯器&#40;變數對應頁面&#41;](../../2014/integration-services/foreach-loop-editor-variable-mappings-page.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [For 迴圈容器](control-flow/for-loop-container.md)  
  
  