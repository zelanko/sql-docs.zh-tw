---
title: XML 工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.xmltask.f1
- sql13.dts.designer.xmltask.general.f1
helpviewer_keywords:
- XML [Integration Services]
- XML task [Integration Services]
ms.assetid: 9f761846-390e-46d5-9db7-858943d40849
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d487c283a463df4b1df7b37953e9f31564240e15
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="xml-task"></a>XML 工作
  XML 工作用於處理 XML 資料。 使用此工作，封裝可以擷取 XML 文件、使用「可延伸樣式表語言轉換」(XSLT) 樣式表和 XPath 運算式將作業套用到文件、合併多個文件，或者驗證、比較更新的文件，並將其儲存至檔案和變數。  
  
 此工作可讓 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝在執行階段動態修改 XML 文件。 您可將 XML 工作用於下列用途：  
  
-   重新格式化 XML 文件。 例如，此工作可以存取位於 XML 檔案的報表，然後動態套用 XSLT 樣式表以自訂文件的呈現方式。  
  
-   選取 XML 文件的小節。 例如，此工作可以存取位於 XML 檔案的報表，然後動態地套用 XPath 運算式來選取文件的小節。 此作業也可以取得和處理文件中的值。  
  
-   合併多個來源的文件。 例如，此工作可以下載多個來源的報表，然後動態地將其合併到一個綜合的 XML 文件。  
  
-   驗證 XML 文件，並可選擇取得詳細的錯誤輸出。 如需詳細資訊，請參閱＜ [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)＞。  
  
 您可以透過使用 XML 來源擷取 XML 文件的值，將 XML 資料包含到資料流程中。 如需詳細資訊，請參閱 [XML 來源](../../integration-services/data-flow/xml-source.md)。  
  
## <a name="xml-operations"></a>XML 作業  
 XML 工作執行的第一個動作是擷取特定的 XML 文件。 此動作內建於 XML 工作中，並且可以自動發生。 擷取的 XML 文件用作 XML 工作執行之作業的資料來源。  
  
 「差異」、「合併」和「修補」的 XML 作業需要兩個運算元。 第一個運算元會指定來源 XML 文件。 第二個運算元也會指定 XML 文件，其內容視作業的需求而定。 例如，差異作業會比較兩個文件；因此，第二個運算元會指定與來源 XML 文件相比較的另一個類似 XML 文件。  
  
 XML 工作可以將變數或「檔案」連接管理員用作其來源，或者在工作屬性中包含 XML 資料。  
  
 如果來源是變數，則指定的變數會包含 XML 文件的路徑。  
  
 如果來源是「檔案」連接管理員，則指定的「檔案」連接管理員會提供來源資訊。 「檔案」連接管理員會在 XML 工作以外另行設定，並在 XML 工作中參考。 「檔案」連接管理員的連接字串會指定 XML 檔案的路徑。 如需相關資訊，請參閱 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)。  
  
 可以設定 XML 工作，以將作業結果儲存到變數或檔案。 如果儲存到檔案，XML 工作則使用「檔案」連接管理員來存取此檔案。 您也可以將差異作業產生的 Diffgram 結果儲存到檔案和變數。  
  
## <a name="predefined-xml-operations"></a>預先定義的 XML 作業  
 XML 工作包括一組預先定義的作業，用於處理 XML 文件。 下表描述這些作業。  
  
|作業|描述|  
|---------------|-----------------|  
|Diff|比較兩份 XML 文件。 差異作業使用來源 XML 文件做為基底文件，將其與第二個 XML 文件相比較，偵測兩者的差異，並將差異寫入 XML Diffgram 文件。 此作業包含用於自訂比較的屬性。|  
|合併式|合併兩份 XML 文件。 「合併」作業使用來源 XML 文件做為基底文件，將第二個文件的內容加入此基底文件。 此作業可以指定基底文件中的合併位置。|  
|修補|將差異作業的輸出 (稱為 Diffgram 文件) 套用到 XML 文件，以新建包含 Diffgram 文件內容的父文件。|  
|Validate|針對「文件類型定義」(DTD) 或「XML 結構描述定義」(XSD) 結構描述來驗證 XML 文件。|  
|XPath|執行 XPath 查詢和評估。|  
|XSLT|在 XML 文件上執行 XSL 轉換。|  
  
### <a name="diff-operation"></a>差異作業  
 視比較要求快還是精確而定，差異作業可設定為使用不同的比較演算法。 作業也可以設定為根據比較文件的大小來自動選取快速或精確比較。  
  
 差異作業包含一組自訂 XML 比較的選項。 下表描述這些選項。  
  
|選項|描述|  
|------------|-----------------|  
|**IgnoreComments**|指定是否要比較註解節點的值。|  
|**IgnoreNamespaces**|指定是否要比較元素的命名空間統一資源識別碼 (URI) 及其屬性名稱的值。 如果此選項設定為 **true**，則本機名稱相同但命名空間不同的兩個元素會被視為一樣。|  
|**IgnorePrefixes**|指定是否要比較元素前置詞和屬性名稱的值。 如果此選項設定為 **true,** ，則本機名稱相同但命名空間 URI 和前置詞不同的兩個元素會被視為一樣。|  
|**IgnoreXMLDeclaration**|指定是否要比較 XML 宣告的值。|  
|**IgnoreOrderOfChildElements**|指定是否要比較子元素順序的值。 如果此選項設定為 **true**，則同層級清單中只有位置不同的子元素會被視為一樣。|  
|**IgnoreWhiteSpaces**|指定是否要比較空白字元的值。|  
|**IgnoreProcessingInstructions**|指定是否要比較處理指示的值。|  
|**IgnoreDTD**|指定是否要忽略 DTD 的值。|  
  
### <a name="merge-operation"></a>合併作業  
 當您使用 XPath 陳述式識別來源文件中的合併位置時，此陳述式預期會傳回單一節點。 如果陳述式傳回多個節點，只會使用第一個節點。 第二個文件的內容會合併到 XPath 查詢傳回的第一個節點之下。  
  
### <a name="xpath-operation"></a>XPath 作業  
 可以將 XPath 作業設定為使用不同類型的 XPath 功能。  
  
-   選取 [評估] 選項以實作 XPath 函數，例如 sum()。  
  
-   選取 **[節點清單]** 選項，將選取的節點當做 XML 片段傳回。  
  
-   選取 **值** 選項以傳回所有選取節點的內部文字值 (串連成一個字串)。  
  
### <a name="validation-operation"></a>驗證作業  
 可以將「驗證」作業設定為使用「文件類型定義」(DTD) 或「XML 結構描述定義」(XSD) 結構描述。  
  
 啟用 **ValidationDetails** 可取得詳細的錯誤輸出。 如需詳細資訊，請參閱＜ [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)＞。  
  
## <a name="xml-document-encoding"></a>XML 文件編碼  
 XML 工作只支援 Unicode 文件的合併。 這表示只能對具有 Unicode 編碼的文件套用「合併」作業。 使用其他編碼將造成 XML 工作失敗。  
  
> [!NOTE]  
>  「差異」和「修補」作業均包含一個選項，可用來忽略第二個運算元 XML 資料中的 XML 宣告，進而能夠在這些作業中使用具有其他編碼方式的文件。  
  
 若要確認 XML 文件是否可用，請檢視 XML 宣告。 宣告必須明確指定 UTF-8 (表示 8 位元的 Unicode 編碼)。  
  
 下列標記顯示 Unicode 8 位元編碼。  
  
 `<?xml version="1.0" encoding="UTF-8"?>`  
  
## <a name="custom-logging-messages-available-on-the-xml-task"></a>XML 工作上可用的自訂記錄訊息  
 下表描述 XML 工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|**XMLOperation**|提供有關工作執行之作業的資訊。|  
  
## <a name="configuration-of-the-xml-task"></a>XML 工作的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [以 XML 工作驗證 XML](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-xml-task"></a>XML 工作的程式設計組態  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.XMLTask.XMLTask>  
  
## <a name="related-tasks"></a>相關工作  
 [設定工作或容器的屬性](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="xml-task-editor-general-page"></a>XML Task Editor (General Page)
  使用 **[XML 工作編輯器]** 對話方塊的 **[一般節點]** ，即可指定作業類型和設定作業。  
  
 若要了解這項工作，請參閱[使用 XML 工作驗證 XML](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)。 如需有關使用 XML 文件和資料的詳細資訊，請參閱 MSDN Library 中的 "[Employing XML in the .NET Framework](http://go.microsoft.com/fwlink/?LinkId=56214)"。  
  
### <a name="static-options"></a>靜態選項  
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
 如果 [Source] 設定為 [直接輸入]，請提供 XML 程式碼，或按一下省略符號按鈕 **(…)**，然後使用 [文件來源編輯器] 對話方塊來提供 XML。  
  
 如果 [來源] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [來源] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
### <a name="operationtype-dynamic-options"></a>OperationType 動態選項  
  
#### <a name="operationtype--validate"></a>OperationType = 驗證  
 指定驗證作業的選項。  
  
 **SaveOperationResult**  
 指定 XML 工作是否儲存驗證作業的輸出。  
  
 **OverwriteDestination**  
 指定是否要覆寫目的地檔案或變數。  
  
 **目的地**  
 選取現有的檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
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
 當此屬性的值為 True 時，會提供詳細的錯誤輸出。 如需詳細資訊，請參閱＜ [Validate XML with the XML Task](../../integration-services/control-flow/validate-xml-with-the-xml-task.md)＞。  
  
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
 如果 [SecondOperandType] 設定為 [直接輸入]，請提供 XML 程式碼，或按一下省略符號按鈕 **(…)**，然後使用 [來源編輯器] 對話方塊來提供 XML。  
  
 如果 [SecondOperandType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [XPathStringSourceType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
#### <a name="operationtype--xslt"></a>OperationType = XSLT  
 指定 XSLT 作業的選項。  
  
 **SaveOperationResult**  
 指定 XML 工作是否儲存 XSLT 作業的輸出。  
  
 **OverwriteDestination**  
 指定是否要覆寫目的地檔案或變數。  
  
 **目的地**  
 如果 [DestinationType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [DestinationType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
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
 如果 [SecondOperandType] 設定為 [直接輸入]，請提供 XML 程式碼，或按一下省略符號按鈕 **(…)**，然後使用 [來源編輯器] 對話方塊來提供 XML。  
  
 如果 [SecondOperandType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [XPathStringSourceType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
#### <a name="operationtype--xpath"></a>OperationType = XPATH  
 指定 XPath 作業的選項。  
  
 **SaveOperationResult**  
 指定 XML 工作是否儲存 XPath 作業的輸出。  
  
 **OverwriteDestination**  
 指定是否要覆寫目的地檔案或變數。  
  
 **目的地**  
 如果 [DestinationType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [DestinationType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
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
 如果 [SecondOperandType] 設定為 [直接輸入]，請提供 XML 程式碼，或按一下省略符號按鈕 **(…)**，然後使用 [來源編輯器] 對話方塊來提供 XML。  
  
 如果 [SecondOperandType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [XPathStringSourceType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
 **PutResultInOneNode**  
 指定是否將結果寫入單一節點。  
  
 **XPathOperation**  
 選取 XPath 結果類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**Evaluation**|傳回 XPath 函數的結果。|  
|**節點清單**|將選取的節點當做 XML 片段傳回。|  
|**值**|傳回所有選取之節點的內部文字值，串連成字串。|  
  
#### <a name="operationtype--merge"></a>OperationType = 合併  
 指定合併作業的選項。  
  
 **XPathStringSourceType**  
 選取 XML 文件的來源類型。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**直接輸入**|設定 XML 文件的來源。|  
|**檔案連接**|選取包含 XML 文件的檔案。|  
|**變數**|設定包含 XML 文件的變數來源。|  
  
 **XPathStringSource**  
 如果 [XPathStringSourceType] 設定為 [直接輸入]，請提供 XML 程式碼，或按一下省略符號按鈕 **(…)**，然後使用 [文件來源編輯器] 對話方塊來提供 XML。  
  
 如果 [XPathStringSourceType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>]，以建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [XPathStringSourceType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>]  建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 當您使用 XPath 陳述式識別來源文件中的合併位置時，此陳述式預期會傳回單一節點。 如果陳述式傳回多個節點，只會使用第一個節點。 第二個文件的內容會合併到 XPath 查詢傳回的第一個節點之下。  
  
 **SaveOperationResult**  
 指定 XML 工作是否儲存合併作業的輸出。  
  
 **OverwriteDestination**  
 指定是否要覆寫目的地檔案或變數。  
  
 **目的地**  
 如果 [DestinationType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [DestinationType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
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
 如果 [SecondOperandType] 設定為 [直接輸入]，請提供 XML 程式碼，或按一下省略符號按鈕 **(…)**，然後使用 [文件來源編輯器] 對話方塊來提供 XML。  
  
 如果 [SecondOperandType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [SecondOperandType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="operationtype--diff"></a>OperationType = Diff  
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
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**IgnoreXMLDeclaration**|指定是否比較 XML 宣告。|  
|**IgnoreDTD**|指定是否忽略文件類型定義 (DTD)。|  
|**IgnoreWhite Spaces**|指定在比較文件時是否忽略空白數量的差異。|  
|**IgnoreNamespaces**|指定是否比較元素的命名空間統一資源識別碼 (URI) 及其屬性名稱。<br /><br /> 注意：如果此選項設定為 **True**，則會將擁有相同本機名稱但命名空間不同的兩個元素視為相同。|  
|**IgnoreProcessingInstructions**|指定是否比較處理指示。|  
|**IgnoreOrderOf ChildElements**|指定是否比較子元素的順序。<br /><br /> 注意：如果此選項設定為 **True**，則會將只是在同層級清單中位置不同的子元素視為相同。|  
|**IgnoreComments**|指定是否比較註解節點。|  
|**IgnorePrefixes**|指定是否比較元素與屬性名稱的前置詞。<br /><br /> 注意：如果此選項設定為 **True**，則會將擁有相同本機名稱但命名空間 URI 與前置詞不同的兩個元素視為相同。|  
  
 **FailOnDifference**  
 指定 Diff 作業失敗時工作是否失敗。  
  
 **SaveDiffGram**  
 指定是否儲存比較結果 DiffGram 文件。  
  
 **SaveOperationResult**  
 指定 XML 工作是否儲存 Diff 作業的輸出。  
  
 **OverwriteDestination**  
 指定是否要覆寫目的地檔案或變數。  
  
 **目的地**  
 如果 [DestinationType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [DestinationType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
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
 如果 [SecondOperandType] 設定為 [直接輸入]，請提供 XML 程式碼，或按一下省略符號按鈕 **(…)**，然後使用 [文件來源編輯器] 對話方塊來提供 XML。  
  
 如果 [SecondOperandType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [SecondOperandType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="operationtype--patch"></a>OperationType = 修補  
 指定修補作業的選項。  
  
 **SaveOperationResult**  
 指定 XML 工作是否儲存修補作業的輸出。  
  
 **OverwriteDestination**  
 指定是否要覆寫目的地檔案或變數。  
  
 **目的地**  
 如果 [DestinationType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [DestinationType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。  
  
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
 如果 [SecondOperandType] 設定為 [直接輸入]，請提供 XML 程式碼，或按一下省略符號按鈕 **(…)**，然後使用 [文件來源編輯器] 對話方塊來提供 XML。  
  
 如果 [SecondOperandType] 設定為 [檔案連線]，請選取檔案連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 如果 [SecondOperandType] 設定為 [變數]，請選取現有的變數，或按一下 [\<新增變數...>] 建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="related-content"></a>相關內容  
  
-   agilebi.com 上的部落格文章： [XML 目的地指令碼元件](http://agilebi.com/jwelch/2007/06/02/xml-destination-script-component/)  
  
-   www.codeplex.com 上的 CodePlex 範例： [處理 XML 資料封裝範例](http://msftisprodsamples.codeplex.com/wikipage?title=SS2008!Process%20XML%20Data%20Package%20Sample&version=10&ProjectName=msftisprodsamples)   
  
  
