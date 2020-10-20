---
description: 一般檔案目的地
title: 一般檔案目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.flatfiledest.f1
- sql13.dts.designer.flatfiledestadapter.connection.f1
- sql13.dts.designer.flatfiledestadapter.mappings.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4b4e23b3f9296153772b1aaead04f48ba5f151a8
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92197117"
---
# <a name="flat-file-destination"></a>一般檔案目的地

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  「一般檔案」目的地會將資料寫入文字檔。 該文字檔的格式可以是使用分隔符號、固定寬度、具有資料列分隔符號的固定寬度，或不齊右。  
  
 您可以利用下列方式設定「一般檔案」目的地：  
  
-   提供寫入任何資料前插入到檔案的文字區塊。 該文字可提供如資料行標題等資訊。  
  
-   指定是否覆寫同名目的地檔案中的資料。  
  
 此目的地使用「一般檔案」連接管理員來存取文字檔。 透過設定「一般檔案」目的地使用之「一般檔案」連接管理員上的屬性，您可以指定「一般檔案」目的地如何格式化並寫入文字檔。 設定「一般檔案」連接管理員時，可以指定有關該檔案以及檔案中每一資料行的資訊。 例如，指定分隔檔案中資料行和資料列的字元，以及各資料行的資料類型和長度。 如需相關資訊，請參閱 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)。  
  
 一般檔案目的地包含 [標頭] 自訂屬性。 屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../integration-services/expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../../integration-services/expressions/use-property-expressions-in-packages.md)和[一般檔案自訂屬性](../../integration-services/data-flow/flat-file-custom-properties.md)。  
  
 此目的地擁有一個輸出。 它不支援錯誤輸出。  
  
## <a name="configuration-of-the-flat-file-destination"></a>一般檔案目的地的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](./set-the-properties-of-a-data-flow-component.md)  
  
-   [一般檔案自訂屬性](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定資料流程元件屬性的資訊，請參閱 [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="flat-file-destination-editor-connection-manager-page"></a>一般檔案目的地編輯器 (連接管理員頁面)
  使用 [一般檔案目的地編輯器] 對話方塊的 [連線管理員] 頁面，來選取目的地的一般檔案連接，以及指定是否要覆寫或附加至現有的目的地檔案。 一般檔案目的地會將資料寫入文字檔。 此文字檔的格式可以是分隔、固定寬度、固定寬度且具有資料列分隔符號或不齊右格式。  
  
### <a name="options"></a>選項。  
 **一般檔案連接管理員**  
 使用清單方塊選取現有的連線管理員，或按一下 [新增]  建立新的連接。  
  
 **新增**  
 使用 [一般檔案格式]  與 [一般檔案連線管理員編輯器]  對話方塊來建立新的連接。  
  
 除了標準一般檔案格式的 [使用分隔符號]、[固定寬度] 和 [不齊右] 等選項之外，[一般檔案格式]  對話方塊還有第四個選項 [有資料列分隔符號的固定寬度]  。 這個選項代表不齊右格式的特殊狀況， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會加入虛擬資料行當做最後資料行。 這個虛擬資料行可確保最終資料行有固定寬度。  
  
 [有資料列分隔符號的固定寬度]  選項不會出現在 [一般檔案連線管理員編輯器]  中。 必要時，您可以在編輯器中模擬這個選項。 若要模擬這個選項，請在 [一般檔案連線管理員編輯器] 的 [一般] 頁面上，針對 [格式] 選取 [不齊右]。 然後在編輯器的 [進階]  頁面上，加入新的虛擬資料行當做最後資料行。  
  
 **覆寫檔案中的資料**  
 指出是要覆寫現有的檔案，還是將資料附加至檔案中。  
  
 **標頭**  
 在寫入任何資料之前，輸入要插入檔案中的文字區塊。 使用此選項來包含其他資訊，例如資料行標題。  
  
 **預覽**  
 使用 [資料檢視]  對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
## <a name="flat-file-destination-editor-mappings-page"></a>一般檔案目的地編輯器 (對應頁面)
  使用 [一般檔案目的地編輯器] 對話方塊的 [對應] 頁面，即可將輸入資料行對應到目的地資料行。  
  
### <a name="options"></a>選項。  
 **可用的輸入資料行**  
 檢視可用的輸入資料行清單。 使用拖放作業，即可將可用的輸入資料行對應到目的地資料行。  
  
 **可用的目的地資料行**  
 檢視可用的目的地資料行清單。 使用拖放作業，即可將可用的目的地資料行對應到輸入資料行。  
  
 **輸入資料行**  
 檢視在這個主題中稍早選取的輸入資料行。 您可以使用 **[可用的輸入資料行]** 清單來變更對應。 選取 [\<ignore>] 即可從輸出中將資料行排除。  
  
 **目的地資料行**  
 檢視每個可用的目的地資料行，不論是否已經對應。  
  
## <a name="see-also"></a>另請參閱  
 [一般檔案來源](../../integration-services/data-flow/flat-file-source.md)   
 [資料流程](../../integration-services/data-flow/data-flow.md)  
  
