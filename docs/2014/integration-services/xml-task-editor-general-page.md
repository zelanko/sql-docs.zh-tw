---
title: XML 工作編輯器 （一般頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmltask.general.f1
helpviewer_keywords:
- XML Task Editor
ms.assetid: b9622c48-3243-4408-a1de-9ba20e32ff70
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aa0f92cc3275810b73d1dbe661a1f8473c7234df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054283"
---
# <a name="xml-task-editor-general-page"></a>XML Task Editor (General Page)
  使用 **[XML 工作編輯器]** 對話方塊的 **[一般節點]** ，即可指定作業類型和設定作業。  
  
 若要了解這個工作，請參閱＜ [XML Task](control-flow/xml-task.md)＞。 如需有關使用 XML 文件和資料的詳細資訊，請參閱 MSDN Library 中的 "[Employing XML in the .NET Framework](https://go.microsoft.com/fwlink/?LinkId=56214)"。  
  
## <a name="static-options"></a>靜態選項  
 **OperationType**  
 從清單中選取作業類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**Validate**|針對「文件類型定義」(DTD) 或「XML 結構描述定義」(XSD) 結構描述來驗證 XML 文件。 選取此選項會在 **[驗證]** 區段中顯示動態選項。|  
|**XSLT**|在 XML 文件上執行 XSL 轉換。 選取此選項會在 **[XSLT]** 區段中顯示動態選項。|  
|**XPATH**|執行 XPath 查詢和評估。 選取此選項會在 **[XPATH]** 區段中顯示動態選項。|  
|**合併式**|合併兩份 XML 文件。 選取此選項會在 **[合併]** 區段中顯示動態選項。|  
|**Diff**|比較兩份 XML 文件。 選取此選項會在 **[Diff]** 區段中顯示動態選項。|  
|**修補**|套用 Diff 作業的輸出，以建立新文件。 選取此選項會在 **[修補]** 區段中顯示動態選項。|  
  
 **SourceType**  
 選取 XML 文件的來源類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 XML 文件的來源。|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **Source**  
 如果 [Source]  設定為 [直接輸入]  ，請提供 XML 程式碼，或按一下省略符號按鈕 ([...])  ，然後使用 [文件來源編輯器]  對話方塊來提供 XML。  
  
 如果 [來源]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [來源]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)。  
  
## <a name="operationtype-dynamic-options"></a>OperationType 動態選項  
  
### <a name="operationtype--validate"></a>OperationType = 驗證  
 指定驗證作業的選項。  
  
 **SaveOperationResult**  
 指定 XML 工作是否儲存驗證作業的輸出。  
  
 **OverwriteDestination**  
 指定是否要覆寫目的地檔案或變數。  
  
 **目的地**  
 選取現有的檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **DestinationType**  
 選取 XML 文件的目的地類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **ValidationType**  
 選取驗證類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**DTD**|使用文件類型定義 (DTD)。|  
|**XSD**|使用 XML 結構描述定義 (XSD) 結構描述。 選取此選項會在 **[ValidationType]** 區段中顯示動態選項。|  
  
 **FailOnValidationFail**  
 指定無法驗證文件時作業是否失敗。  
  
 **ValidationDetails**  
 當此屬性的值為 True 時，會提供詳細的錯誤輸出。 如需詳細資訊，請參閱＜ [Validate XML with the XML Task](control-flow/validate-xml-with-the-xml-task.md)＞。  
  
### <a name="validationtype-dynamic-options"></a>ValidationType 動態選項  
  
#### <a name="validationtype--xsd"></a>ValidationType = XSD  
 **SecondOperandType**  
 選取第二個 XML 文件的來源類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 XML 文件的來源。|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **SecondOperand**  
 如果 [SecondOperandType]  設定為 [直接輸入]  ，請提供 XML 程式碼，或按一下省略符號按鈕 ([...])  ，然後使用 [來源編輯器]  對話方塊來提供 XML。  
  
 如果 [SecondOperandType]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [XPathStringSourceType]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]   建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)。  
  
### <a name="operationtype--xslt"></a>OperationType = XSLT  
 指定 XSLT 作業的選項。  
  
 **SaveOperationResult**  
 指定 XML 工作是否儲存 XSLT 作業的輸出。  
  
 **OverwriteDestination**  
 指定是否要覆寫目的地檔案或變數。  
  
 **目的地**  
 如果 [DestinationType]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [DestinationType]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)。  
  
 **DestinationType**  
 選取 XML 文件的目的地類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **SecondOperandType**  
 選取第二個 XML 文件的來源類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 XML 文件的來源。|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **SecondOperand**  
 如果 [SecondOperandType]  設定為 [直接輸入]  ，請提供 XML 程式碼，或按一下省略符號按鈕 ([...])  ，然後使用 [來源編輯器]  對話方塊來提供 XML。  
  
 如果 [SecondOperandType]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [XPathStringSourceType]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]   建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)。  
  
### <a name="operationtype--xpath"></a>OperationType = XPATH  
 指定 XPath 作業的選項。  
  
 **SaveOperationResult**  
 指定 XML 工作是否儲存 XPath 作業的輸出。  
  
 **OverwriteDestination**  
 指定是否要覆寫目的地檔案或變數。  
  
 **目的地**  
 如果 [DestinationType]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [DestinationType]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)。  
  
 **DestinationType**  
 選取 XML 文件的目的地類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **SecondOperandType**  
 選取第二個 XML 文件的來源類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 XML 文件的來源。|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **SecondOperand**  
 如果 [SecondOperandType]  設定為 [直接輸入]  ，請提供 XML 程式碼，或按一下省略符號按鈕 ([...])  ，然後使用 [來源編輯器]  對話方塊來提供 XML。  
  
 如果 [SecondOperandType]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [XPathStringSourceType]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]   建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)。  
  
 **PutResultInOneNode**  
 指定是否將結果寫入單一節點。  
  
 **XPathOperation**  
 選取 XPath 結果類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**Evaluation**|傳回 XPath 函數的結果。|  
|**節點清單**|將選取的節點當做 XML 片段傳回。|  
|**值**|傳回所有選取之節點的內部文字值，串連成字串。|  
  
### <a name="operationtype--merge"></a>OperationType = 合併  
 指定合併作業的選項。  
  
 **XPathStringSourceType**  
 選取 XML 文件的來源類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 XML 文件的來源。|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **XPathStringSource**  
 如果 [XPathStringSourceType]  設定為 [直接輸入]  ，請提供 XML 程式碼，或按一下省略符號按鈕 ([...])  ，然後使用 [文件來源編輯器]  對話方塊來提供 XML。  
  
 如果 [XPathStringSourceType]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  ，以建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [XPathStringSourceType]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]   建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)  
  
 當您使用 XPath 陳述式識別來源文件中的合併位置時，此陳述式預期會傳回單一節點。 如果陳述式傳回多個節點，只會使用第一個節點。 第二個文件的內容會合併到 XPath 查詢傳回的第一個節點之下。  
  
 **SaveOperationResult**  
 指定 XML 工作是否儲存合併作業的輸出。  
  
 **OverwriteDestination**  
 指定是否要覆寫目的地檔案或變數。  
  
 **目的地**  
 如果 [DestinationType]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [DestinationType]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)。  
  
 **DestinationType**  
 選取 XML 文件的目的地類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **SecondOperandType**  
 選取第二份 XML 文件的目的地類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 XML 文件的來源。|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **SecondOperand**  
 如果 [SecondOperandType]  設定為 [直接輸入]  ，請提供 XML 程式碼，或按一下省略符號按鈕 ([...])  ，然後使用 [文件來源編輯器]  對話方塊來提供 XML。  
  
 如果 [SecondOperandType]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [SecondOperandType]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--diff"></a>OperationType = Diff  
 指定 Diff 作業的選項。  
  
 **DiffAlgorithm**  
 選取比較文件時要使用的 Diff 演算法。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**Auto**|讓 XML 工作決定使用快速或精確演算法。|  
|**快速**|使用快速但比較不精確的 Diff 演算法。|  
|**精確**|使用精確 Diff 演算法。|  
  
 **Diff 選項**  
 設定要套用至 Diff 作業的 Diff 選項。 選項會在下表中列出。  
  
|值|描述|  
|-----------|-----------------|  
|**IgnoreXMLDeclaration**|指定是否比較 XML 宣告。|  
|**IgnoreDTD**|指定是否忽略文件類型定義 (DTD)。|  
|**IgnoreWhite Spaces**|指定在比較文件時是否忽略空白數量的差異。|  
|**IgnoreNamespaces**|指定是否比較元素的命名空間統一資源識別碼 (URI) 及其屬性名稱。<br /><br /> 注意:如果此選項設定為`True`，兩個項目擁有相同本機名稱但不同的命名空間會視為相同。|  
|**IgnoreProcessingInstructions**|指定是否比較處理指示。|  
|**IgnoreOrderOf ChildElements**|指定是否比較子元素的順序。<br /><br /> 注意:如果此選項設定為`True`，差別只在於同層級清單中位置的子元素視為相同。|  
|**IgnoreComments**|指定是否比較註解節點。|  
|**IgnorePrefixes**|指定是否比較元素與屬性名稱的前置詞。<br /><br /> 注意:如果您將此選項設定為`True`，擁有相同本機名稱但不同的命名空間 Uri 與前置詞，兩個元素視為相同。|  
  
 **FailOnDifference**  
 指定 Diff 作業失敗時工作是否失敗。  
  
 **SaveDiffGram**  
 指定是否儲存比較結果 DiffGram 文件。  
  
 **SaveOperationResult**  
 指定 XML 工作是否儲存 Diff 作業的輸出。  
  
 **OverwriteDestination**  
 指定是否要覆寫目的地檔案或變數。  
  
 **目的地**  
 如果 [DestinationType]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [DestinationType]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)。  
  
 **DestinationType**  
 選取 XML 文件的目的地類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **SecondOperandType**  
 選取 XML 文件的目的地類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 XML 文件的來源。|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **SecondOperand**  
 如果 [SecondOperandType]  設定為 [直接輸入]  ，請提供 XML 程式碼，或按一下省略符號按鈕 ([...])  ，然後使用 [文件來源編輯器]  對話方塊來提供 XML。  
  
 如果 [SecondOperandType]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [SecondOperandType]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--patch"></a>OperationType = 修補  
 指定修補作業的選項。  
  
 **SaveOperationResult**  
 指定 XML 工作是否儲存修補作業的輸出。  
  
 **OverwriteDestination**  
 指定是否要覆寫目的地檔案或變數。  
  
 **目的地**  
 如果 [DestinationType]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [DestinationType]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)。  
  
 **DestinationType**  
 選取 XML 文件的目的地類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **SecondOperandType**  
 選取 XML 文件的目的地類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 XML 文件的來源。|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **SecondOperand**  
 如果 [SecondOperandType]  設定為 [直接輸入]  ，請提供 XML 程式碼，或按一下省略符號按鈕 ([...])  ，然後使用 [文件來源編輯器]  對話方塊來提供 XML。  
  
 如果 [SecondOperandType]  設定為 [檔案連線]  ，請選取檔案連線管理員，或按一下 [\<新增連線...>]  建立新的連線管理員。  
  
 **相關主題：** [檔案連線管理員](connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 如果 [SecondOperandType]  設定為 [變數]  ，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [運算式頁面](expressions/expressions-page.md)  
  
  
