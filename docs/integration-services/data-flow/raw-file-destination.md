---
description: Raw File Destination
title: 原始檔案目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rawfiledest.f1
- sql13.dts.designer.rawfiledestinationconnectionmanager.f1
- sql13.dts.designer.rawfiledestinationcolumns.f1
helpviewer_keywords:
- append options [Integration Services]
- destinations [Integration Services], Raw File
- raw data [Integration Services]
- writing raw data
- Raw File destination
ms.assetid: d311b458-aefc-4b4d-b1a1-4c0ebbb34214
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 27b28672540d25fe84573c37004161992d3d3827
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "92194185"
---
# <a name="raw-file-destination"></a>Raw File Destination

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  「原始檔案」目的地會將原始資料寫入檔案。 由於資料的格式對於目的地而言是原生的，因此資料不需翻譯，也幾乎不需要剖析。 這表示，「原始檔案」目的地可比其他目的地更快地寫入資料，例如「一般檔案」和 OLE DB 目的地。  
  
 除了將原始資料寫入檔案之外，您也可以使用原始檔案目的地產生僅包含資料行 (僅中繼資料的檔案) 的空白原始檔案，而不必執行封裝。 您可以使用原始檔案來源擷取之前由目的地撰寫的原始資料。 您也可以將原始檔案來源指向僅中繼資料的檔案。  
  
 原始檔案格式包含排序資訊。 原始檔案目的地會儲存所有排序資訊，包括字串資料行的比較旗標。 原始檔案來源會讀取並接受排序資訊。 您可以使用進階編輯器，選擇將原始檔案來源設定為忽略檔案中的排序旗標。 如需比較旗標的詳細資訊，請參閱 [比較字串資料](../../integration-services/data-flow/comparing-string-data.md)。  
  
 您可以利用下列方式設定「原始檔案」目的地：  
  
-   指定存取模式，可以是在其中寫入「原始檔案」目的地的檔案名稱或包含該檔案名稱的變數。  
  
-   指示「原始檔案」目的地是將資料附加至具有相同名稱的現有檔案還是建立新檔案。  
  
 「原始檔案」目的地通常用於寫入在各個封裝執行之間已部份處理之資料的中介結果。 儲存原始資料表示「原始檔案」來源可快速讀取資料，然後在將這些資料載入到其最終目的地前作進一步的轉換。 例如，封裝可執行多次，每次均將原始資料寫入檔案。 稍後，另一個封裝可使用「原始檔案」來源從每份檔案讀取，並使用「聯集全部」轉換將資料合併到一個資料集中，然後在將這些資料載入到其最終目的地 (例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表) 之前，套用可摘要資料的其他轉換。  
  
> [!NOTE]  
>  「原始檔案」目的地支援 Null 資料但不支援二進位大型物件 (BLOB) 資料。  
  
> [!NOTE]  
>  「原始檔案」目的地不使用連接管理員。  
  
 此來源具有一個規則輸入。 它不支援錯誤輸出。  
  
## <a name="append-and-new-file-options"></a>附加和新增檔案選項  
 WriteOption 屬性包含將資料附加至現有檔案或建立新檔案的選項。  
  
 下表描述 WriteOption 屬性的可用選項。  
  
|選項|描述|  
|------------|-----------------|  
|附加|將資料附加至現有檔案。 附加資料的中繼資料必須符合檔案格式。|  
|永遠建立|永遠建立新檔案。|  
|建立一次|建立新檔案。 如果該檔案存在，元件就會失敗。|  
|截斷與附加|截斷一個現有檔案，然後將資料寫入該檔案。 附加資料的中繼資料必須符合檔案格式。|  
  
 以下是關於附加資料的重要項目：  
  
-   將資料附加到現有的原始檔案時，不會重新排序資料。  
  
     您需要確定已排序的索引鍵維持正確的順序。  
  
-   將資料附加到現有的原始檔案時，不會變更檔案中繼資料 (排序資訊)。  
  
 例如，封裝會讀取以 ProductKey (PK) 排序的資料。 封裝資料流程會將資料附加到現有的原始資料。 封裝第一次執行時，會收到三個資料列 (PK 1000、1100、1200)。 原始檔案現在包含下列資料。  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
 封裝第二次執行時，會收到兩個資料列 (PK 1001、1300)。 原始檔案現在包含下列資料。  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
-   1001, productD  
  
-   1300, productE  
  
 新的資料會附加到原始檔案結尾，而且已排序的索引鍵 (PK) 會失序。 此外，附加作業不會變更檔案中繼資料 (排序資訊)。 如果您使用原始檔案來源讀取檔案，此元件會指出，即使檔案中的資料不再處於正確的順序，檔案仍以 PK 排序。  
  
 若要在附加資料時保持已排序的索引鍵處於正確的順序，您可以設計封裝資料流程，如下所示：  
  
1.  使用來源 A 擷取新的資料列。  
  
2.  使用來源 B，從 RawFile1 擷取現有的資料列。  
  
3.  使用聯集全部 (Union All) 轉換結合來源 A 與來源 B 的輸入。  
  
4.  以 PK 排序。  
  
5.  使用原始檔案目的地寫入 RawFile2。  
  
     在資料流程中，由於 RawFile1 是讀取來源，因此遭到鎖定。  
  
6.  將 RawFile1 取代成 RawFile2。  
  
### <a name="using-the-raw-file-destination-in-a-loop"></a>在迴圈中使用原始檔案目的地  
 如果使用「原始檔案」目的地的資料流程位於迴圈中，您可以建立一次該檔案，然後在迴圈重複時將資料附加至檔案。 若要將資料附加至檔案，附加的資料必須符合現有檔案的格式。  
  
 若要在迴圈的第一次反覆運算中建立檔案，然後在迴圈的後續反覆運算中附加資料列，您需要在設計階段執行下列動作：  
  
1.  將 WriteOption 屬性設為 [CreateOnce] 或 [CreateAlways]，然後執行一次迴圈的反覆運算。 檔案就會建立， 這可確保附加資料的中繼資料與該檔案相符。  
  
2.  將 WriteOption 屬性重設為 [Append] ValidateExternalMetadata 屬性設定為 [False]。  
  
 如果您使用 [TruncateAppend] 選項，而不是 [Append] 選項，它就會截斷在任何先前反覆運算中新增的資料列，然後附加新的資料列。 使用 [TruncateAppend] 選項也會要求資料符合檔案格式。  
  
## <a name="configuration-of-the-raw-file-destination"></a>原始檔案目的地的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](./set-the-properties-of-a-data-flow-component.md)  
  
-   [原始檔案自訂屬性](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 如需如何設定此元件屬性的資訊，請參閱 [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="related-content"></a>相關內容  
 Sqlservercentral.com 上的部落格文章： [Raw Files Are Awesome](https://www.sqlservercentral.com/blogs/31-days-of-ssis-%e2%80%93-raw-files-are-awesome-131)(原始檔案令人敬畏)。  
  
## <a name="raw-file-destination-editor-connection-manager-page"></a>原始檔案目的地編輯器 (連接管理員頁面)
  使用原始檔案目的地編輯器設定原始檔案目的地將，以便將原始資料寫入至檔案。  
  
 **您想要做什麼事？**  
  
-   [開啟原始檔案目的地編輯器](#open)  
  
-   [設定連接管理員索引標籤上的選項](#connection)  
  
-   [設定資料行索引標籤上的選項](#mapping)  
  
###  <a name="open-the-raw-file-destination-editor"></a><a name="open"></a> 開啟原始檔案目的地編輯器  
  
1.  將「原始檔案」目的地加入至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]封裝。  
  
2.  以滑鼠右鍵按一下此元件，然後按一下 **[編輯]**。  
  
###  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> 設定連接管理員索引標籤上的選項  
 **存取模式**  
 選取指定檔案名稱的方式。 選取 **[檔案名稱]** 直接輸入檔案名稱和路徑，或是選取 **[來自變數的檔案名稱]** 指定包含檔案名稱的變數。  
  
 **[檔案名稱]** 或 **[變數名稱]**  
 輸入原始檔案的名稱和路徑，或是選取包含檔案名稱的變數。  
  
 **寫入選項**  
 選取用來建立和寫入檔案的方法。  
  
 **產生初始的原始檔案**  
 按一下此按鈕可以產生僅包含資料行 (僅中繼資料的檔案) 的空白原始檔案，而不必執行封裝。 此檔案包含您在 **[原始檔案目的地編輯器]** 之 **[資料行]** 頁面上選取的資料行。 您可以將原始檔案來源指向這個僅中繼資料的檔案。  
  
 當您按一下 **[產生初始原始檔案]** 時，隨即顯示訊息方塊。 按一下 **[確定]** ，繼續建立檔案。 按一下 **[取消]** ，在 **[資料行]** 頁面上選取不同的資料行清單。  
  
###  <a name="set-options-on-the-columns-tab"></a><a name="mapping"></a> 設定資料行索引標籤上的選項  
 **可用的輸入資料行**  
 選取要寫入至原始檔案的一個或多個輸入資料行。  
  
 **輸入資料行**  
 當您在 **[可用的輸入資料行]** 底下選取資料表時，輸入資料行會自動加入此資料表中，或者您可以直接在此資料表中選取輸入資料行。  
  
 **輸出別名**  
 指定要做為輸出資料行使用的替代名稱。  
  
## <a name="raw-file-destination-editor-columns-page"></a>原始檔案目的地編輯器 (資料行頁面)
  使用原始檔案目的地編輯器設定原始檔案目的地將，以便將原始資料寫入至檔案。  
  
 **您想要做什麼事？**  
  
-   [開啟原始檔案目的地編輯器](#open)  
  
-   [設定連接管理員索引標籤上的選項](#connection)  
  
-   [設定資料行索引標籤上的選項](#mapping)  
  
###  <a name="open-the-raw-file-destination-editor"></a><a name="open"></a> 開啟原始檔案目的地編輯器  
  
1.  將「原始檔案」目的地加入至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]封裝。  
  
2.  以滑鼠右鍵按一下此元件，然後按一下 **[編輯]**。  
  
###  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> 設定連接管理員索引標籤上的選項  
 **存取模式**  
 選取指定檔案名稱的方式。 選取 **[檔案名稱]** 直接輸入檔案名稱和路徑，或是選取 **[來自變數的檔案名稱]** 指定包含檔案名稱的變數。  
  
 **[檔案名稱]** 或 **[變數名稱]**  
 輸入原始檔案的名稱和路徑，或是選取包含檔案名稱的變數。  
  
 **寫入選項**  
 選取用來建立和寫入檔案的方法。  
  
 **產生初始的原始檔案**  
 按一下此按鈕可以產生僅包含資料行 (僅中繼資料的檔案) 的空白原始檔案，而不必執行封裝。 您可以將原始檔案來源指向僅中繼資料的檔案。  
  
 當您按一下該按鈕時，資料行的清單便會出現。 您可以按一下 [取消]，然後修改資料行，或按一下 [確定]，以繼續建立該檔案。  
  
###  <a name="set-options-on-the-columns-tab"></a><a name="mapping"></a> 設定資料行索引標籤上的選項  
 **可用的輸入資料行**  
 選取要寫入至原始檔案的一個或多個輸入資料行。  
  
 **輸入資料行**  
 當您在 **[可用的輸入資料行]** 底下選取資料表時，輸入資料行會自動加入此資料表中，或者您可以直接在此資料表中選取輸入資料行。  
  
 **輸出別名**  
 指定要做為輸出資料行使用的替代名稱。  
  
## <a name="see-also"></a>另請參閱  
 [原始檔案來源](../../integration-services/data-flow/raw-file-source.md)   
 [資料流程](../../integration-services/data-flow/data-flow.md)  
  
