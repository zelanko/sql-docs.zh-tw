---
title: XML 工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmltask.f1
helpviewer_keywords:
- XML [Integration Services]
- XML task [Integration Services]
ms.assetid: 9f761846-390e-46d5-9db7-858943d40849
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e89f4835b95b1fe497df32ad9f773be84ccb161b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "75232731"
---
# <a name="xml-task"></a>XML 工作
  XML 工作用於處理 XML 資料。 使用此工作，封裝可以擷取 XML 文件、使用「可延伸樣式表語言轉換」(XSLT) 樣式表和 XPath 運算式將作業套用到文件、合併多個文件，或者驗證、比較更新的文件，並將其儲存至檔案和變數。  
  
 此工作可讓 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝在執行階段動態修改 XML 文件。 您可將 XML 工作用於下列用途：  
  
-   重新格式化 XML 文件。 例如，此工作可以存取位於 XML 檔案的報表，然後動態套用 XSLT 樣式表以自訂文件的呈現方式。  
  
-   選取 XML 文件的小節。 例如，此工作可以存取位於 XML 檔案的報表，然後動態地套用 XPath 運算式來選取文件的小節。 此作業也可以取得和處理文件中的值。  
  
-   合併多個來源的文件。 例如，此工作可以下載多個來源的報表，然後動態地將其合併到一個綜合的 XML 文件。  
  
-   驗證 XML 文件，並可選擇取得詳細的錯誤輸出。 如需詳細資訊，請參閱＜ [Validate XML with the XML Task](xml-task.md)＞。  
  
 您可以透過使用 XML 來源擷取 XML 文件的值，將 XML 資料包含到資料流程中。 如需詳細資訊，請參閱 [XML 來源](../data-flow/xml-source.md)。  
  
## <a name="xml-operations"></a>XML 作業  
 XML 工作執行的第一個動作是擷取特定的 XML 文件。 此動作內建於 XML 工作中，並且可以自動發生。 擷取的 XML 文件用作 XML 工作執行之作業的資料來源。  
  
 「差異」、「合併」和「修補」的 XML 作業需要兩個運算元。 第一個運算元會指定來源 XML 文件。 第二個運算元也會指定 XML 文件，其內容視作業的需求而定。 例如，差異作業會比較兩個文件；因此，第二個運算元會指定與來源 XML 文件相比較的另一個類似 XML 文件。  
  
 XML 工作可以將變數或「檔案」連接管理員用作其來源，或者在工作屬性中包含 XML 資料。  
  
 如果來源是變數，則指定的變數會包含 XML 文件的路徑。  
  
 如果來源是「檔案」連接管理員，則指定的「檔案」連接管理員會提供來源資訊。 「檔案」連接管理員會在 XML 工作以外另行設定，並在 XML 工作中參考。 「檔案」連接管理員的連接字串會指定 XML 檔案的路徑。 如需相關資訊，請參閱 [File Connection Manager](../connection-manager/file-connection-manager.md)。  
  
 可以設定 XML 工作，以將作業結果儲存到變數或檔案。 如果儲存到檔案，XML 工作則使用「檔案」連接管理員來存取此檔案。 您也可以將差異作業產生的 Diffgram 結果儲存到檔案和變數。  
  
## <a name="predefined-xml-operations"></a>預先定義的 XML 作業  
 XML 工作包括一組預先定義的作業，用於處理 XML 文件。 下表描述這些作業。  
  
|作業|描述|  
|---------------|-----------------|  
|Diff|比較兩份 XML 文件。 差異作業使用來源 XML 文件做為基底文件，將其與第二個 XML 文件相比較，偵測兩者的差異，並將差異寫入 XML Diffgram 文件。 此作業包含用於自訂比較的屬性。|  
|合併|合併兩份 XML 文件。 「合併」作業使用來源 XML 文件做為基底文件，將第二個文件的內容加入此基底文件。 此作業可以指定基底文件中的合併位置。|  
|Patch|將差異作業的輸出 (稱為 Diffgram 文件) 套用到 XML 文件，以新建包含 Diffgram 文件內容的父文件。|  
|Validate|針對「文件類型定義」(DTD) 或「XML 結構描述定義」(XSD) 結構描述來驗證 XML 文件。|  
|XPath|執行 XPath 查詢和評估。|  
|XSLT|在 XML 文件上執行 XSL 轉換。|  
  
### <a name="diff-operation"></a>差異作業  
 視比較要求快還是精確而定，差異作業可設定為使用不同的比較演算法。 作業也可以設定為根據比較文件的大小來自動選取快速或精確比較。  
  
 差異作業包含一組自訂 XML 比較的選項。 下表描述這些選項。  
  
|選項|描述|  
|------------|-----------------|  
|**IgnoreComments**|指定是否要比較註解節點的值。|  
|**IgnoreNamespaces**|指定是否要比較元素的命名空間統一資源識別碼 (URI) 及其屬性名稱的值。 如果此選項設定為 `true`，則本機名稱相同但命名空間不同的兩個元素會被視為一樣。|  
|**IgnorePrefixes**|指定是否要比較元素前置詞和屬性名稱的值。 如果此選項設定為 `true,`，則本機名稱相同但命名空間 URI 和前置詞不同的兩個元素會被視為一樣。|  
|**IgnoreXMLDeclaration**|指定是否要比較 XML 宣告的值。|  
|**IgnoreOrderOfChildElements**|指定是否要比較子元素順序的值。 如果此選項設定為 `true`，則同層級清單中只有位置不同的子元素會被視為一樣。|  
|**IgnoreWhiteSpaces**|指定是否要比較空白字元的值。|  
|**IgnoreProcessingInstructions**|指定是否要比較處理指示的值。|  
|**IgnoreDTD**|指定是否要忽略 DTD 的值。|  
  
### <a name="merge-operation"></a>合併作業  
 當您使用 XPath 陳述式識別來源文件中的合併位置時，此陳述式預期會傳回單一節點。 如果陳述式傳回多個節點，只會使用第一個節點。 第二個文件的內容會合併到 XPath 查詢傳回的第一個節點之下。  
  
### <a name="xpath-operation"></a>XPath 作業  
 可以將 XPath 作業設定為使用不同類型的 XPath 功能。  
  
-   選取 [評估]  選項以實作 XPath 函數，例如 sum()。  
  
-   選取 **[節點清單]** 選項，將選取的節點當做 XML 片段傳回。  
  
-   選取 **值** 選項以傳回所有選取節點的內部文字值 (串連成一個字串)。  
  
### <a name="validation-operation"></a>驗證作業  
 可以將「驗證」作業設定為使用「文件類型定義」(DTD) 或「XML 結構描述定義」(XSD) 結構描述。  
  
 啟用 `ValidationDetails` 可取得詳細的錯誤輸出。 如需詳細資訊，請參閱＜ [Validate XML with the XML Task](xml-task.md)＞。  
  
## <a name="xml-document-encoding"></a>XML 文件編碼  
 XML 工作只支援 Unicode 文件的合併。 這表示只能對具有 Unicode 編碼的文件套用「合併」作業。 使用其他編碼將造成 XML 工作失敗。  
  
> [!NOTE]  
>  「差異」和「修補」作業均包含一個選項，可用來忽略第二個運算元 XML 資料中的 XML 宣告，進而能夠在這些作業中使用具有其他編碼方式的文件。  
  
 若要確認 XML 文件是否可用，請檢視 XML 宣告。 宣告必須明確指定 UTF-8 (表示 8 位元的 Unicode 編碼)。  
  
 下列標記顯示 Unicode 8 位元編碼。  
  
 `<?xml version="1.0" encoding="UTF-8"?>`  
  
## <a name="custom-logging-messages-available-on-the-xml-task"></a>XML 工作上可用的自訂記錄訊息  
 下表描述 XML 工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)和[自訂訊息以進行記錄](../custom-messages-for-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`XMLOperation`|提供有關工作執行之作業的資訊。|  
  
## <a name="configuration-of-the-xml-task"></a>XML 工作的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [[XML 工作編輯器] &#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [以 XML 工作驗證 XML](xml-task.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-xml-task"></a>XML 工作的程式設計組態  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.XMLTask.XMLTask>  
  
## <a name="related-tasks"></a>相關工作  
 [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>相關內容  
  
-   agilebi.com 上的部落格文章： [XML 目的地指令碼元件](http://agilebi.com/jwelch/2007/06/02/xml-destination-script-component/)  
  
-   [www.codeplex.com](www.codeplex.com) 上的 CodePlex 範例： [處理 XML 資料封裝範例](https://msftisprodsamples.codeplex.com/wikipage?title=SS2008!Process%20XML%20Data%20Package%20Sample&version=10&ProjectName=msftisprodsamples)  
  
