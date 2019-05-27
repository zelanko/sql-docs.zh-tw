---
title: 複製並貼上資料 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.pastepreviewdb.f1
ms.assetid: 2f8d8b3d-810b-4c31-98f2-341015e13da8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad25ecae16a9b5e5f32554350a315156e9818241
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086973"
---
# <a name="copy-and-paste-data-ssas-tabular"></a>複製及貼上資料 (SSAS 表格式)
  您可以從外部應用程式複製資料表的資料，並將其貼入模型設計師中新的資料表或現有的資料表。 您從 [剪貼簿] 貼入的資料必須是 HTML 格式，例如從 Excel 或 Word 複製的資料。 模型設計師將會自動偵測並套用資料類型至貼上的資料。 您也可以手動修改資料類型或資料行的顯示格式設定。  
  
 與含資料來源連接的資料表不同的是，貼上的資料表不具備連接名稱或來源資料屬性。 貼上的資料保存於 Model.bim 檔中。 儲存專案或 Model.bim 檔時，也會儲存貼上的資料。  
  
 當部署模型時，無論部署是否處理該模型，也會一併部署貼上的資料。  
  
 本主題的章節：  
  
-   [必要條件](#bkmk_prerequisites)  
  
-   [貼上資料](#bkmk_paste_data)  
  
-   [貼上預覽對話方塊](#bkmk_paste_preview)  
  
##  <a name="bkmk_prerequisites"></a> 必要條件  
 貼上資料時有一些限制：  
  
-   貼上的資料表不能超過 10,000 個資料列。  
  
-   貼上的資料表不能進行資料分割。  
  
-   DirectQuery 模式不支援貼上的資料表。  
  
-   只有當處理的資料表原先是透過從 [剪貼簿] 貼上資料而建立時，才可以使用 **[貼上新增]** 和 **[貼上取代]** 選項。 您無法使用 **[貼上新增]** 和 **[貼上取代]** ，將資料加入其他資料來源類型之匯入資料的資料表。  
  
-   當您使用 **[貼上新增]** 或 **[貼上取代]** 時，新的資料必須與原始資料的資料行數目完全相同。 您貼上或附加的資料行，最好也與目的地資料表是相同或相容的資料類型。 在某些情況下，您可以使用不同的資料類型，但會顯示 **類型不符** 的錯誤。  
  
##  <a name="bkmk_paste_data"></a> 貼上資料  
  
#### <a name="to-paste-data-into-the-designer"></a>將資料貼入設計師  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，按一下 **[編輯]** 功能表，然後按一下下列其中一項：  
  
    -   按一下 **[貼上]** ，將 [剪貼簿] 中的內容貼入新的資料表中。  
  
    -   按一下 **[貼上新增]** ，將 [剪貼簿] 的內容當做額外的資料列貼入選取的資料表中。 新的資料列將會加入至資料表的結尾。  
  
    -   按一下 **[貼上取代]** ，以 [剪貼簿] 的內容取代選取的資料表。 所有現有的資料行標頭名稱依然會在資料表中，並且保留關聯性。  
  
##  <a name="bkmk_paste_preview"></a> 貼上預覽對話方塊  
 **[貼上預覽]** 對話方塊可讓您查看已複製到設計師視窗之資料的預覽，並確認資料已正確複製。 若要存取此對話方塊，請將以資料表為基礎的 HTML 格式資料複製到剪貼簿，然後在設計師中，按一下 [編輯] 功能表，再按一下 [貼上]、[貼上新增] 或 [貼上取代]。 只有在透過從剪貼簿複製並貼上而建立的資料表中加入或取代資料時，才可以使用 **[貼上新增]** 和 **[取代貼上]** 選項。 您不能使用 **[貼上新增]** 或 **[取代貼上]** ，將資料加入至匯入資料的資料表中。  
  
 根據您是將資料貼入全新的資料表、貼入現有的資料表並以新資料取代現有資料，或附加到現有資料表，此對話方塊的選項都不同。  
  
### <a name="paste-to-new-table"></a>貼入新資料表  
 **資料表名稱**  
 指定將會在設計師中建立之資料表的名稱。  
  
 **要貼上的資料**  
 顯示將加入到目的地資料表的 [剪貼簿] 內容範例。  
  
### <a name="paste-append"></a>[貼上新增]  
 **資料表中的現有資料**  
 顯示資料表中現有資料的範例，以便讓您確認資料行、資料類型等。  
  
 **要貼上的資料**  
 顯示剪貼簿內容的範例。 此資料將會附加現有資料。  
  
### <a name="paste-replace"></a>[貼上取代]  
 **資料表中的現有資料**  
 顯示資料表中現有資料的範例，以便讓您確認資料行、資料類型等。  
  
 **要貼上的資料**  
 顯示剪貼簿內容的範例。 目的地資料表中的現有資料將會遭到刪除，並將新資料列插入資料表中。  
  
## <a name="see-also"></a>另請參閱  
 [匯入資料 (SSAS 表格式)](import-data-ssas-tabular.md)   
 [支援的資料來源 &#40;SSAS 表格式&#41;](tabular-models/data-sources-supported-ssas-tabular.md)   
 [設定資料行的資料類型 &#40;SSAS 表格式&#41;](tabular-models/set-the-data-type-of-a-column-ssas-tabular.md)  
  
  
