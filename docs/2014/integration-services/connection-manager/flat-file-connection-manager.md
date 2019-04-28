---
title: 一般檔案連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
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
ms.openlocfilehash: 4466ebd24647520c7cbba2bf0baa93a0f60a72bf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833808"
---
# <a name="flat-file-connection-manager"></a>一般檔案連接管理員
  「一般檔案」連接管理員可讓封裝存取一般檔案中的資料。 例如，「一般檔案」來源與目的地可以使用「一般檔案」連接管理員來擷取並載入資料。  
  
 「一般檔案」連接管理員僅可存取一個檔案。 若要參考多個檔案，請使用「多個一般檔案」連接管理員，而非「一般檔案」連接管理員。 如需詳細資訊，請參閱 [Multiple Flat Files Connection Manager](multiple-flat-files-connection-manager.md)。  
  
## <a name="column-length"></a>資料行長度  
 依預設，「一般檔案」連接管理員會將字串資料行的長度設定成 50 個字元。 在 [一般檔案連接管理員編輯器]  對話方塊中，您可以評估取樣資料，並自動調整這些資料行的長度，以避免資料遭截斷或超出資料行寬度。 此外，除非接著在一般檔案來源或轉換中調整資料行長度，否則字串資料行在整個資料流程中的資料行長度將維持不變。 如果這些字串資料行對應到較窄的目的地資料行，使用者介面中將會出現警告。 此外，執行階段中也可能發生因為資料截斷所產生的錯誤。 若要避免錯誤或資料截斷，您可以調整資料行的大小，使其與一般檔案連接管理員、一般檔案來源或轉換中的目的地資料行相容。 若要修改輸出資料行的長度，您設定`Length`上的輸出資料行的屬性**輸入與輸出屬性**索引標籤**進階編輯器** 對話方塊。  
  
 如果在加入及設定使用「一般檔案」連接管理員的一般檔案來源之後，在該連接管理員中更新資料行長度，您就不需要手動調整一般檔案來源中輸出資料行的大小。 在您開啟 **[一般檔案來源]** 對話方塊時，一般檔案來源會提供一個用來同步化資料行中繼資料的選項。  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>設定一般檔案連接管理員  
 當您新增一般檔案連接管理員加入封裝時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]建立連接管理員，會解析為在執行階段的一般檔案連接、 設定一般檔案 」 連接屬性，以及將一般檔案連接管理員加入`Connections`封裝的集合。  
  
 連接管理員的 `ConnectionManagerType` 屬性會設為 `FLATFILE`。  
  
 根據預設，「一般檔案」連接管理員一律會檢查未加引號之資料中的資料列分隔符號，並在找到資料列分隔符號時開始一個新資料列。 這可讓連接管理員正確地剖析資料列缺少資料行欄位的檔案。  
  
 在某些情況下，停用此功能可能會提升封裝效能。 您可以藉由設定 「 一般檔案連接管理員屬性停用此功能**AlwaysCheckForRowDelimiters**至`False`。  
  
 您可以利用下列方式設定「一般檔案」連接管理員：  
  
-   指定要使用的檔案、地區設定及字碼頁。 地區設定用於解譯區分地區設定的資料 (如日期)，字碼頁用於將字串資料轉換為 Unicode。  
  
-   指定檔案格式。 您可以使用分隔的、固定寬度或不齊右格式。  
  
-   指定標頭資料列、資料列和資料行分隔符號。 資料行分隔符號可以在檔案層級設定，並在資料行層級覆寫。  
  
-   指示檔案中的第一個資料列是否包含資料行名稱。  
  
-   指定文字限定詞字元。 每個資料行都可以設定為識別文字限定詞。  
  
     現在支援使用限定詞字元，將限定詞字元內嵌到限定字串中。 文字限定詞的雙執行個體會解譯成常值 (該字串的單一執行個體)。 例如，文字限定詞如果是單引號，而輸入資料為 'abc'、'def'、'g'hi'，則輸出資料為 abc、def、g'hi。  
  
-   在個別的資料行上設定屬性，例如名稱、資料類型和最大寬度。  
  
 您可以針對一般檔案連接管理員來設定 ConnectionString 屬性，其方式是在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 [屬性] 視窗中指定運算式。 為避免驗證錯誤，請執行下列操作。  
  
-   當您使用運算式指定檔案時，請在 [一般檔案連接管理員編輯器]  的 [檔案名稱] 方塊中加入檔案路徑。  
  
-   在「一般檔案」連接管理員上將 **DelayValidation** 屬性設定為 [True] 。  
  
 您可以透過具有「一般檔案」目的地的「一般檔案」連接管理員，使用運算式在執行階段建立檔案名稱。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [一般檔案連線管理員編輯器 &#40;[一般]頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [一般檔案連線管理員編輯器 &#40;[資料行] 頁面&#41;](../flat-file-connection-manager-editor-columns-page.md)  
  
-   [一般檔案連線管理員編輯器 &#40;[進階] 頁面&#41;](../flat-file-connection-manager-editor-advanced-page.md)  
  
-   [一般檔案連接管理員編輯器 &#40;[預覽] 頁面&#41;](../flat-file-connection-manager-editor-preview-page.md)  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
  
