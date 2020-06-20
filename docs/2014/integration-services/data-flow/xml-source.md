---
title: XML 來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmlsource.f1
helpviewer_keywords:
- sources [Integration Services], XML
- XML source [Integration Services]
- XML Source Editor
ms.assetid: 68c27ea5-e93d-4e26-bfb2-d967ca0a5282
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 0cd1817bbf9b3cdca4181e8fb32dfbe76fd59dc7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939199"
---
# <a name="xml-source"></a>XML 來源
  XML 來源會讀取 XML 資料檔案，並將資料填入來源輸出中的資料行。  
  
 XML 檔案中的資料經常會包括階層式關聯性。 例如，XML 資料檔案可代表目錄以及目錄中的項目。 在資料能夠進入資料程序之前，必須先決定 XML 資料檔案中各元素之間的關聯性，並且為檔案中各元素產生輸出。  
  
## <a name="schemas"></a>結構描述  
 XML 來源使用結構描述解譯 XML 資料。 XML 來源支援使用 XML 結構描述定義 (XSD) 檔或內嵌結構描述，將 XML 資料翻譯成表格格式。 如果您使用 [XML 來源編輯器]  對話方塊設定 XML 來源，則使用者介面可從指定的 XML 資料檔案產生 XSD。  
  
> [!NOTE]  
>  不支援 DTD。  
  
 結構描述僅可支援單一命名空間，而不支援結構描述集合。  
  
> [!NOTE]  
>  XML 來源不會根據 XSD 驗證 XML 檔案中的資料。  
  
## <a name="xml-source-editor"></a>XML 來源編輯器  
 XML 檔案中的資料經常會包括階層式關聯性。 [XML 來源編輯器]  對話方塊會使用指定的結構描述產生 XML 來源輸出。 您可以指定 XSD 檔、使用內嵌結構描述，或從指定的 XML 資料檔案產生 XSD。 結構描述必須於設計階段提供。  
  
 XML 來源會藉由為包含 XML 檔案中其他元素的每項元素建立輸出的方式，從 XML 資料產生表格式結構。 例如，如果 XML 資料代表目錄以及目錄中的項目，則 XML 來源會為目錄以及目錄所包含的每一種項目建立輸出。 每一個項目的輸出將包含該項目屬性的輸出資料行。  
  
 為了提供有關輸出中資料的階層式關聯性的資訊，XML 來源會在輸出中加入識別每一個子元素所屬父元素的資料行。 若使用含有不同項目類型的目錄範例，則各項目可能會有識別其所屬目錄的資料行值。  
  
 XML 來源會為每一個元素建立輸出，但您不需使用所有輸出。 您可以刪除任何不要使用的輸出，或不要將它連接到下游元件。  
  
 XML 來源還會產生輸出名稱，以確保名稱不會模糊不清。 這些名稱可能很長，且可能不會以對您來說實用的方式識別輸出。 您可以重新命名輸出，只要其名稱保持唯一即可。 您也可以修改資料類型和輸出資料行的長度。  
  
 XML 來源會針對每一項輸出加入錯誤輸出。 依預設，錯誤輸出中的資料行的資料類型為 Unicode 字串 (DT_WSTR)，且其長度為 255，不過您可以藉由修改資料類型和長度的方式設定錯誤輸出中的資料行。  
  
 如果 XML 資料檔案包含 XSD 中沒有的元素，則會略過這些元素且不會產生其輸出。 換言之，如果 XML 資料檔案遺漏了 XSD 中出現的元素，則輸出會包含擁有 Null 值的資料行。  
  
 從 XML 資料檔案擷取資料時，該資料會轉換為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型。 但是，XML 來源無法將 XML 資料轉換成 DT_TIME2 或 DT_DBTIMESTAMP2 資料類型，因為此來源不支援這些資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](integration-services-data-types.md)。  
  
 XSD 或內嵌結構描述可能會指定元素的資料類型；如果未指定，則 [XML 來源編輯器]  對話方塊會指派 Unicode 字串資料類型 (DT_WSTR) 給包含該元素的輸出中的資料行，並將資料行長度設定為 255 個字元。  
  
 如果結構描述指定元素的最大長度，輸出資料行的長度會設為此值。 如果最大長度大於元素轉換成的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型支援的長度，則資料會截斷成該資料類型的最大長度。 例如，如果字串長度為 5000，因為 DT_WSTR 資料類型的最大長度是 4000 個字元，則字串會截斷成 4000 個字元；同樣地，位元組資料會截斷成 DT_BYTES 資料類型的最大長度 8000 個字元。 如果結構描述指定無最大長度，則具有其中一種資料類型的預設資料行長度會設為 255。 XML 來源中的資料截斷會使用與其他資料流程元件中的截斷相同的方式來處理。 如需詳細資訊，請參閱 [處理資料中的錯誤](error-handling-in-data.md)。  
  
 您可以修改資料類型和資料行長度。 如需詳細資訊，請參閱 [Integration Services 資料類型](integration-services-data-types.md)。  
  
## <a name="configuration-of-the-xml-source"></a>設定 XML 來源  
 XML 來源支援三種不同的資料存取模式。 您可以指定 XML 資料檔案的檔案位置、包含檔案位置的變數，或包含 XML 資料的變數。  
  
 XML 來源包括 `XMLData` 和 `XMLSchemaDefinition` 自訂屬性；屬性運算式可以在載入封裝時更新這些屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../expressions/use-property-expressions-in-packages.md)和 [XML 來源自訂屬性](xml-source-custom-properties.md)。  
  
 XML 來源支援多項規則輸出和多項錯誤輸出。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含用來設定 XML 來源的 [XML 來源編輯器]  對話方塊。 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中即提供此對話方塊。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需 [XML 來源編輯器] **** 對話方塊中可設定屬性的詳細資訊，請按一下下列其中一個主題：  
  
-   [XML 來源編輯器 &#40;[連線管理員] 頁面&#41;](../xml-source-editor-connection-manager-page.md)  
  
-   [XML 來源編輯器 &#40;[資料行] 頁面&#41;](../xml-source-editor-columns-page.md)  
  
-   [XML 來源編輯器 &#40;[錯誤輸出] 頁面&#41;](../xml-source-editor-error-output-page.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../common-properties.md)  
  
-   [XML 來源自訂屬性](xml-source-custom-properties.md)  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>相關工作  
 [使用 XML 來源來擷取資料](xml-source.md)  
  
## <a name="related-content"></a>相關內容  
 [使用 XML 檔案設定 SSIS 封裝](https://www.sqlshack.com/using-xml-file-configure-ssis-package/)的技術文章。  
  
  
