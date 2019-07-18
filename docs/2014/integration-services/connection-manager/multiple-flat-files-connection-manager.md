---
title: 多個一般檔案連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7235f5f333ac7bb4520a6244e103baafba343ea3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833699"
---
# <a name="multiple-flat-files-connection-manager"></a>多個一般檔案連接管理員
  「多個一般檔案」連接管理員可讓封裝存取多個一般檔案中的資料。 例如，當資料流程工作位於迴圈容器 (如 For 迴圈容器) 內時，「一般檔案」來源可以使用「多個一般檔案」連接管理員。 在此容器的每一個迴圈上，「一般檔案」來源會從「多個一般檔案」連接管理員提供的下一個檔案名稱中載入資料。  
  
 當您新增多個一般檔案連接管理員加入封裝時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]建立連接，將會解析為在執行階段，設定在多個一般檔案連接管理員屬性的多個一般檔案連接管理員和將多個一般檔案連接管理員加入`Connections`封裝的集合。  
  
 連接管理員的 `ConnectionManagerType` 屬性會設為 `MULTIFLATFILE`。  
  
 您可以利用下列方式設定「多個一般檔案」連接管理員：  
  
-   指定要使用的檔案、地區設定和字碼頁。 地區設定用於解譯區分地區設定的資料 (如日期)，字碼頁用於將字串資料轉換為 Unicode。  
  
-   指定檔案格式。 您可以使用分隔的、固定寬度或不齊右格式。  
  
-   指定標頭資料列、資料列和資料行分隔符號。 資料行分隔符號可以在檔案層級設定，並在資料行層級覆寫。  
  
-   指出檔案中的第一個資料列是否包含資料行名稱。  
  
-   指定文字限定詞字元。 每個資料行都可以設定為識別文字限定詞。  
  
-   在個別的資料行上設定屬性，例如名稱、資料類型和最大寬度。  
  
 如果「多個一般檔案」連接管理員參考多個檔案，則檔案的路徑會以垂直線 (|) 字元隔開。 連接管理員的 `ConnectionString` 屬性具有下列格式：  
  
 \<*path*>|\<*path*>  
  
 您也可以使用萬用字元來指定多個檔案。 例如，若要參考磁碟機 C 上的所有文字檔，值`ConnectionString`屬性可以設定為 c:\\*.txt。  
  
 如果「多個一般檔案」連接管理員參考多個檔案，則所有檔案必須具有相同的格式。  
  
 依預設，「多個一般檔案」連接管理員會將字串資料行的長度設定成 50 個字元。 在 **[多個一般檔案連接管理員編輯器]** 對話方塊中，您可以評估取樣資料，並自動調整這些資料行的長度，以避免資料遭截斷或超出資料行寬度。 除非在一般檔案來源或轉換中調整資料行長度，否則在整個資料流程中，資料行長度將維持不變。 如果這些資料行對應到較窄的目的資料行，使用者介面中將會出現警告，而且在執行階段中可能發生因為資料截斷所產生的錯誤。 您可以調整資料行的大小，使其與一般檔案連接管理員、一般檔案來源或轉換中的目的地資料行相容。 若要修改輸出資料行的長度，您設定`Length`上的輸出資料行的屬性**輸入與輸出屬性**索引標籤**進階編輯器** 對話方塊。  
  
 如果在加入及設定使用「多個一般檔案」連接管理員的一般檔案來源之後，在該連接管理員中更新資料行長度，您就不需要手動調整一般檔案來源中輸出資料行的大小。 在您開啟 **[一般檔案來源]** 對話方塊時，一般檔案來源會提供一個用來同步化資料行中繼資料的選項。  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>設定多個一般檔案連接管理員  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [多個一般檔案連接管理員編輯器 &#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [多個一般檔案連接管理員編輯器 &#40;資料行頁面&#41;](../multiple-flat-files-connection-manager-editor-columns-page.md)  
  
-   [多個一般檔案連接管理員編輯器 &#40;進階頁面&#41;](../multiple-flat-files-connection-manager-editor-advanced-page.md)  
  
-   [多個一般檔案連接管理員編輯器 &#40;預覽頁面&#41;](../multiple-flat-files-connection-manager-editor-preview-page.md)  
  
 如需以程式設計方式設定連接管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>另請參閱  
 [[一般檔案來源]](../data-flow/flat-file-source.md)   
 [一般檔案目的地](../data-flow/flat-file-destination.md)   
 [Integration Services &#40;SSIS&#41; 連接](integration-services-ssis-connections.md)  
  
  
