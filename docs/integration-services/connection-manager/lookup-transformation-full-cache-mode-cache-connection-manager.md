---
title: 查閱轉換完整快取模式 - 快取連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation [Integration Services]
ms.assetid: 58bc7611-5fb5-4113-9742-10959e06b94c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d612cb08431c5618d5d3e6e7c0574d79bf43000e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728202"
---
# <a name="lookup-transformation-full-cache-mode---cache-connection-manager"></a>查閱轉換完整快取模式 - 快取連線管理員

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  您可以將查閱轉換設定為使用完整快取模式以及快取連接管理員。 在完整快取模式中，參考資料集會在查閱轉換執行之前載入快取。  
  
> [!NOTE]  
>  快取連接管理員不支援二進位大型物件 (BLOB) 資料類型 DT_TEXT、DT_NTEXT 和 DT_IMAGE。 如果參考資料集包含 BLOB 資料類型，則在您執行封裝時元件會失敗。 您可以使用 **[快取連接管理員編輯器]** 修改資料行資料類型。 如需詳細資訊，請參閱 [快取連線管理員編輯器](../../integration-services/connection-manager/cache-connection-manager-editor.md)。  
  
 查閱轉換會藉由聯結已連接資料來源輸入資料行中的資料與參考資料集中的資料行來執行查閱。 如需相關資訊，請參閱 [Lookup Transformation](../../integration-services/data-flow/transformations/lookup-transformation.md)。  
  
 您可以使用下列其中一個項目來產生參考資料集：  
  
-   快取檔案 (.caw)  
  
     將快取連接管理員設定為從現有的快取檔案讀取資料。  
  
-   資料流程中的已連接資料來源  
  
     使用快取轉換，將資料流程中已連接資料來源的資料寫入快取連接管理員。 資料永遠會儲存在記憶體中。  
  
     您必須將查閱轉換加入個別的資料流程中。 如此可在查閱轉換執行之前，先讓快取轉換擴展快取連接管理員。 資料流程可能位於相同的封裝或兩個不同的封裝。  
  
     如果資料流程位於相同的封裝，請使用優先順序條件約束來連接資料流程。 如此可在查閱轉換執行之前，先讓快取轉換執行。  
  
     如果資料流程位於不同的封裝，可以使用執行封裝工作從父封裝呼叫子封裝。 您可以將多個執行封裝工作加入父封裝中的時序容器工作，藉此呼叫多個子封裝。  
  
 您可以藉由使用下列其中一種方法，在多個查閱轉換之間共用儲存在快取中的參考資料集：  
  
-   將單一封裝中的查閱轉換設定為使用相同的快取連接管理員。  
  
-   將不同封裝中的快取連接管理員設定為使用相同的快取檔案。  
  
 如需詳細資訊，請參閱下列主題：  
  
-   [快取轉換](../../integration-services/data-flow/transformations/cache-transform.md)  
  
-   [快取連接管理員](../../integration-services/connection-manager/cache-connection-manager.md)  
  
-   [優先順序條件約束](../../integration-services/control-flow/precedence-constraints.md)  
  
-   [執行封裝工作](../../integration-services/control-flow/execute-package-task.md)  
  
-   [時序容器](../../integration-services/control-flow/sequence-container.md)  
  
 如需示範如何使用快取連接管理員在完整快取模式下實作查閱轉換的視訊，請參閱[如何：在完整快取模式中實作查閱轉換 (SQL Server 影片)](https://go.microsoft.com/fwlink/?LinkId=131031)。  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-in-one-package-by-using-cache-connection-manager-and-a-data-source-in-the-data-flow"></a>若要使用快取連接管理員和資料流程中的資料來源在單一封裝中以完整快取模式實作查閱轉換  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中開啟 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，然後開啟封裝。  
  
2.  在 [控制流程]  索引標籤上加入兩個資料流程工作，然後使用綠色的連接子來連接這些工作：  
  
3.  在第一個資料流程中加入快取轉換轉換，然後將該轉換連接到資料來源。  
  
     視需要設定資料來源。  
  
4.  按兩下 [快取轉換]，然後在 [快取轉換編輯器]  中，按一下 [連線管理員]  頁面上的 [新增]  ，建立新的快取連線管理員。  
  
5.  按一下 [快取連線管理員編輯器]  對話方塊的 [資料行]  索引標籤，然後使用 [索引位置]  選項，指定哪些資料行是索引資料行。  
  
     如果是非索引資料行，索引位置為 0。 如果是索引資料行，則索引位置是循序的正數。  
  
    > [!NOTE]  
    >  當查閱轉換是設定為使用快取連接管理員，則只有參考資料集中的索引資料行可以對應到輸入資料行。 而且，所有的索引資料行都必須進行對應。 如需詳細資訊，請參閱 [快取連線管理員編輯器](../../integration-services/connection-manager/cache-connection-manager-editor.md)。  
  
6.  若要將快取儲存至檔案，請在 [快取連線管理員編輯器]  的 [一般]  索引標籤上，藉由設定下列選項來設定快取連線管理員：  
  
    -   選取 [使用檔案快取]  。  
  
    -   在 [檔案名稱]  中，輸入檔案路徑或是按一下 [瀏覽]  選取檔案。  
  
         如果輸入的檔案路徑不存在，系統就會在執行封裝時建立該檔案。  
  
    > [!NOTE]  
    >  封裝保護等級不會套用至快取檔案。 如果快取檔案包含機密資訊，請使用存取控制清單 (ACL) 限制對其中儲存檔案的位置或資料夾的存取權。 您應該只啟用特定帳戶的存取權。 如需詳細資訊，請參閱 [對封裝使用之檔案的存取權](../../integration-services/security/security-overview-integration-services.md#files)。  
  
7.  視需要設定快取轉換。 如需詳細資訊，請參閱[快取轉換編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/transformations/cache-transformation-editor-connection-manager-page.md) 和[快取轉換編輯器 &#40;對應頁面&#41;](../../integration-services/data-flow/transformations/cache-transformation-editor-mappings-page.md)。  
  
8.  藉由執行下列工作，在第二個資料流程中加入查閱轉換，然後設定該轉換：  
  
    1.  從來源或先前的轉換將連接子拖曳到查閱轉換，以便將查閱轉換連接到資料流程。  
  
        > [!NOTE]  
        >  查閱轉換如果連接到包含空白日期欄位的一般檔案，則查閱轉換可能不會驗證。 此轉換是否會驗證將取決於一般檔案的連線管理員是否已設定為保留 null 值。 若要確保查閱轉換會驗證，請在 **[一般檔案來源編輯器]** 的 **[連線管理員]** 頁面上，選取 **[將來源的 Null 值保留為資料流程中的 Null 值]** 選項。  
  
    2.  按兩下來源或前一個轉換以設定元件。  
  
    3.  按兩下查閱轉換，然後在 [查閱轉換編輯器]  的 [一般]  頁面上，選取 [完整快取]  。  
  
    4.  在 [連接類型]  區域中選取 [快取連線管理員]  。  
  
    5.  從 [指定如何處理無相符項目的資料列]  清單中選取錯誤處理選項。  
  
    6.  在 [連接]  頁面的 [快取連線管理員]  清單上，選取快取連線管理員。  
  
    7.  按一下 **[資料行]** 頁面，然後從 **[可用的輸入資料行]** 清單，拖曳至少一個資料行至 **[可用的查閱資料行]** 清單中的資料行。  
  
        > [!NOTE]  
        >  「查閱」轉換會自動對應具有相同名稱和相同資料類型的資料行。  
  
        > [!NOTE]  
        >  資料行必須具有要對應的相符資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
    8.  在 [可用的查閱資料行]  清單中選取資料行。 然後在 [查閱作業]  清單中，指定查閱資料行的值是否要取代輸入資料行中的值，或要寫入至新的資料行。  
  
    9. 若要設定錯誤輸出，按一下 **[錯誤輸出]** 頁面，然後設定錯誤處理選項。 如需詳細資訊，請參閱[查閱轉換編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)。  
  
    10. 按一下 [確定]  ，將變更儲存至查閱轉換。  
  
9. 執行封裝。  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-in-two-packages-by-using-cache-connection-manager-and-a-data-source-in-the-data-flow"></a>使用快取連接管理員和資料流程中的資料來源在兩個封裝中以完整快取模式實作查閱轉換  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中開啟 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，然後開啟兩個封裝。  
  
2.  在每個封裝的 [控制流程] 索引標籤上，加入資料流程工作。  
  
3.  在父封裝中，將快取轉換轉換加入至資料流程，然後將該轉換連接到資料來源。  
  
     視需要設定資料來源。  
  
4.  按兩下快取轉換，然後在 [快取轉換編輯器]  中，按一下 [連線管理員]  頁面上的 [新增]  ，建立新的快取連線管理員。  
  
5.  在 [快取連線管理員編輯器]  的 [一般]  索引標籤上，藉由設定下列選項來設定快取連線管理員：  
  
    -   選取 [使用檔案快取]  。  
  
    -   在 [檔案名稱]  中，輸入檔案路徑或是按一下 [瀏覽]  選取檔案。  
  
         如果輸入的檔案路徑不存在，系統就會在執行封裝時建立該檔案。  
  
    > [!NOTE]  
    >  封裝保護等級不會套用至快取檔案。 如果快取檔案包含機密資訊，請使用存取控制清單 (ACL) 限制對其中儲存檔案的位置或資料夾的存取權。 您應該只啟用特定帳戶的存取權。 如需詳細資訊，請參閱 [對封裝使用之檔案的存取權](../../integration-services/security/security-overview-integration-services.md#files)。  
  
6.  按一下 [資料行]  索引標籤，然後使用 [索引位置]  選項，指定哪些資料行是索引資料行。  
  
     如果是非索引資料行，索引位置為 0。 如果是索引資料行，則索引位置是循序的正數。  
  
    > [!NOTE]  
    >  當查閱轉換是設定為使用快取連接管理員，則只有參考資料集中的索引資料行可以對應到輸入資料行。 而且，所有的索引資料行都必須進行對應。 如需詳細資訊，請參閱 [快取連線管理員編輯器](../../integration-services/connection-manager/cache-connection-manager-editor.md)。  
  
7.  視需要設定快取轉換。 如需詳細資訊，請參閱[快取轉換編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/transformations/cache-transformation-editor-connection-manager-page.md) 和[快取轉換編輯器 &#40;對應頁面&#41;](../../integration-services/data-flow/transformations/cache-transformation-editor-mappings-page.md)。  
  
8.  請執行下列其中一項作業，以擴展用於第二個封裝中的快取連接管理員：  
  
    -   執行父封裝。  
  
    -   按兩下在步驟 4 中所建立的快取連線管理員，再按一下 [資料行]  ，選取資料列，然後按下 CTRL+C 來複製資料行中繼資料。  
  
9. 在子封裝中，以滑鼠右鍵按一下 [連線管理員]  區域，然後按一下 [新增連接]  ，在 [加入 SSIS 連線管理員]  對話方塊中選取 [CACHE]  ，然後按一下 [加入]  ，藉此建立快取連線管理員。  
  
     [連線管理員]  區域會出現在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 設計師的 [控制流程]  、[資料流程]  和 [事件處理常式]  索引標籤底部。  
  
10. 在 [快取連線管理員編輯器]  的 [一般]  索引標籤上，藉由設定下列選項，將快取連線管理員設定為從選取的快取檔案讀取資料：  
  
    -   選取 [使用檔案快取]  。  
  
    -   在 [檔案名稱]  中，輸入檔案路徑或是按一下 [瀏覽]  選取檔案。  
  
    > [!NOTE]  
    >  封裝保護等級不會套用至快取檔案。 如果快取檔案包含機密資訊，請使用存取控制清單 (ACL) 限制對其中儲存檔案的位置或資料夾的存取權。 您應該只啟用特定帳戶的存取權。 如需詳細資訊，請參閱[對封裝使用之檔案的存取權](../../integration-services/security/security-overview-integration-services.md#files)。  
  
11. 如果已在步驟 8 中複製了資料行中繼資料，請按一下 [資料行]  ，選取空白資料列，然後按下 CTRL+V 來貼上資料行中繼資料。  
  
12. 藉由執行下列工作加入查閱轉換，然後設定該轉換：  
  
    1.  從來源或先前的轉換將連接子拖曳到查閱轉換，以便將查閱轉換連接到資料流程。  
  
        > [!NOTE]  
        >  查閱轉換如果連接到包含空白日期欄位的一般檔案，則查閱轉換可能不會驗證。 此轉換是否會驗證將取決於一般檔案的連線管理員是否已設定為保留 null 值。 若要確保查閱轉換會驗證，請在 **[一般檔案來源編輯器]** 的 **[連線管理員]** 頁面上，選取 **[將來源的 Null 值保留為資料流程中的 Null 值]** 選項。  
  
    2.  按兩下來源或前一個轉換以設定元件。  
  
    3.  按兩下 [查閱轉換]，然後在 [查閱轉換編輯器]  的 [一般]  頁面上，選取 [完整快取]  。  
  
    4.  在 [連接類型]  區域中選取 [快取連線管理員]  。  
  
    5.  從 [指定如何處理無相符項目的資料列]  清單，針對沒有相符項目的資料列選取錯誤處理選項。  
  
    6.  在 [連接]  頁面的 [快取連線管理員]  清單上，選取您加入的快取連線管理員。  
  
    7.  按一下 **[資料行]** 頁面，然後從 **[可用的輸入資料行]** 清單，拖曳至少一個資料行至 **[可用的查閱資料行]** 清單中的資料行。  
  
        > [!NOTE]  
        >  「查閱」轉換會自動對應具有相同名稱和相同資料類型的資料行。  
  
        > [!NOTE]  
        >  資料行必須具有要對應的相符資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
    8.  在 [可用的查閱資料行]  清單中選取資料行。 然後在 [查閱作業]  清單中，指定查閱資料行的值是否要取代輸入資料行中的值，或要寫入至新的資料行。  
  
    9. 若要設定錯誤輸出，按一下 **[錯誤輸出]** 頁面，然後設定錯誤處理選項。 如需詳細資訊，請參閱[查閱轉換編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)。  
  
    10. 按一下 [確定]  ，將變更儲存至查閱轉換。  
  
13. 開啟父封裝，在控制流程中加入執行封裝工作，然後將工作設定為呼叫子封裝。 如需詳細資訊，請參閱 [執行封裝工作](../../integration-services/control-flow/execute-package-task.md)。  
  
14. 執行封裝。  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-by-using-cache-connection-manager-and-an-existing-cache-file"></a>使用快取連接管理員和現有的快取檔案以完整快取模式實作查閱轉換  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中開啟 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，然後開啟封裝。  
  
2.  以滑鼠右鍵按一下 [連線管理員]  區域，然後按一下 [新增連接]  。  
  
     [連線管理員]  區域會出現在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 設計師的 [控制流程]  、[資料流程]  和 [事件處理常式]  索引標籤底部。  
  
3.  在 [加入 SSIS 連線管理員]  對話方塊中選取 [CACHE]  ，然後按一下 [加入]  加入快取連線管理員。  
  
4.  按兩下 [快取連線管理員]，開啟 [快取連線管理員編輯器]  。  
  
5.  在 [快取連線管理員編輯器]  的 [一般]  索引標籤上，藉由設定下列選項來設定快取連線管理員：  
  
    -   選取 [使用檔案快取]  。  
  
    -   在 [檔案名稱]  中，輸入檔案路徑或是按一下 [瀏覽]  選取檔案。  
  
    > [!NOTE]  
    >  封裝保護等級不會套用至快取檔案。 如果快取檔案包含機密資訊，請使用存取控制清單 (ACL) 限制對其中儲存檔案的位置或資料夾的存取權。 您應該只啟用特定帳戶的存取權。 如需詳細資訊，請參閱 [對封裝使用之檔案的存取權](../../integration-services/security/security-overview-integration-services.md#files)。  
  
6.  按一下 [資料行]  索引標籤，然後使用 [索引位置]  選項，指定哪些資料行是索引資料行。  
  
     如果是非索引資料行，索引位置為 0。 如果是索引資料行，則索引位置是循序的正數。  
  
    > [!NOTE]  
    >  當查閱轉換是設定為使用快取連接管理員，則只有參考資料集中的索引資料行可以對應到輸入資料行。 而且，所有的索引資料行都必須進行對應。 如需詳細資訊，請參閱[快取連線管理員編輯器](../../integration-services/connection-manager/cache-connection-manager-editor.md)。  
  
7.  在 [控制流程]  索引標籤上，將資料流程工作加入封裝，然後將查閱轉換加入資料流程。  
  
8.  您可以利用下列方式設定查閱轉換：  
  
    1.  從來源或先前的轉換將連接子拖曳到查閱轉換，以便將查閱轉換連接到資料流程。  
  
        > [!NOTE]  
        >  查閱轉換如果連接到包含空白日期欄位的一般檔案，則查閱轉換可能不會驗證。 此轉換是否會驗證將取決於一般檔案的連線管理員是否已設定為保留 null 值。 若要確保查閱轉換會驗證，請在 **[一般檔案來源編輯器]** 的 **[連線管理員]** 頁面上，選取 **[將來源的 Null 值保留為資料流程中的 Null 值]** 選項。  
  
    2.  按兩下來源或前一個轉換以設定元件。  
  
    3.  按兩下 [查閱轉換]，然後在 [查閱轉換編輯器]  的 [一般]  頁面上，選取 [完整快取]  。  
  
    4.  在 [連接類型]  區域中選取 [快取連線管理員]  。  
  
    5.  從 [指定如何處理無相符項目的資料列]  清單，針對沒有相符項目的資料列選取錯誤處理選項。  
  
    6.  在 [連接]  頁面的 [快取連線管理員]  清單上，選取您加入的快取連線管理員。  
  
    7.  按一下 **[資料行]** 頁面，然後從 **[可用的輸入資料行]** 清單，拖曳至少一個資料行至 **[可用的查閱資料行]** 清單中的資料行。  
  
        > [!NOTE]  
        >  「查閱」轉換會自動對應具有相同名稱和相同資料類型的資料行。  
  
        > [!NOTE]  
        >  資料行必須具有要對應的相符資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
    8.  在 [可用的查閱資料行]  清單中選取資料行。 然後在 [查閱作業]  清單中，指定查閱資料行的值是否要取代輸入資料行中的值，或要寫入至新的資料行。  
  
    9. 若要設定錯誤輸出，按一下 **[錯誤輸出]** 頁面，然後設定錯誤處理選項。 如需詳細資訊，請參閱[查閱轉換編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)。  
  
    10. 按一下 [確定]  ，將變更儲存至查閱轉換。  
  
9. 執行封裝。  
  
## <a name="see-also"></a>另請參閱  
 [使用 OLE DB 連接管理員，以完整快取模式來實作查閱轉換](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)   
 [以沒有快取或部分快取模式來實作查閱](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)   
 [Integration Services 轉換](../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
