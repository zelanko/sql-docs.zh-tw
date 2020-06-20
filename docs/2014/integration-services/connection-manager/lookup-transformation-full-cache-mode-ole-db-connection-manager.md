---
title: 使用 OLE DB 連線管理員，以完整快取模式來執行查閱轉換 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation [Integration Services]
ms.assetid: c4150e1b-bdff-4f7a-af4c-3401c34def83
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4a1aaee0abdd8ecde6c0db857c4ce006a91cccf6
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84920635"
---
# <a name="implement-a-lookup-transformation-in-full-cache-mode-using-the-ole-db-connection-manager"></a>使用 OLE DB 連接管理員，以完整快取模式來實作查閱轉換
  您可以將查閱轉換設定為使用完整快取模式以及 OLE DB 連接管理員。 在完整快取模式中，參考資料集會在查閱轉換執行之前載入快取。  
  
 查閱轉換會藉由聯結已連接資料來源輸入資料行中的資料與參考資料集中的資料行來執行查閱。 如需相關資訊，請參閱 [Lookup Transformation](../data-flow/transformations/lookup-transformation.md)。  
  
 當您將查閱轉換設定為使用 OLE DB 連接管理員時，可以選取資料表、檢視或 SQL 查詢來產生參考資料集。  
  
### <a name="to-implement-a-lookup-transformation-in-full-cache-mode-by-using-ole-db-connection-manager"></a>使用 OLE DB 連接管理員以完整快取模式實作查閱轉換  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案，然後在 [方案總管] 中按兩下該封裝。  
  
2.  在 **[資料流程]** 索引標籤中，將查閱轉換從 **[工具箱]** 拖曳至設計介面。  
  
3.  從來源或先前的轉換將連接子拖曳到查閱轉換，以便將查閱轉換連接到資料流程。  
  
    > [!NOTE]  
    >  查閱轉換如果連接到包含空白日期欄位的一般檔案，則查閱轉換可能不會驗證。 此轉換是否會驗證將取決於一般檔案的連線管理員是否已設定為保留 null 值。 若要確保查閱轉換會驗證，請在 **[一般檔案來源編輯器]** 的 **[連線管理員]** 頁面上，選取 **[將來源的 Null 值保留為資料流程中的 Null 值]** 選項。  
  
4.  按兩下來源或前一個轉換以設定元件。  
  
5.  按兩下查閱轉換，然後在 [查閱轉換編輯器]  的 [一般]  頁面上，選取 [完整快取]  。  
  
6.  在 **[連接類型]** 區域中，選取 **[OLE DB 連接管理員]** 。  
  
7.  在 **[指定如何處理無相符項目的資料列]** 清單中，針對沒有相符項目的資料列選取錯誤處理選項。  
  
8.  在 [連接] 頁面上，從 **[OLE DB 連接管理員]** 清單中選取連接管理員，或按一下 **[新增]** 建立新的連接管理員。 如需相關資訊，請參閱 [OLE DB Connection Manager](ole-db-connection-manager.md)。  
  
9. 執行下列其中一項工作：  
  
    -   按一下 **[使用資料表或檢視]** ，然後選取資料表或檢視，或按一下 **[新增]** 建立資料表或檢視。  
  
         -或-  
  
    -   按一下 **[使用 SQL 查詢的結果]** ，然後在 **[SQL 命令]** 視窗中建立查詢，或是按一下 **[建立查詢]** ，使用 **[查詢產生器]** 提供的圖形工具來建立查詢。  
  
         -或-  
  
    -   或者，按一下 **[瀏覽]** ，從檔案匯入 SQL 陳述式。  
  
     若要驗證 SQL 查詢，請按一下 **[剖析查詢]** 。  
  
     若要檢視資料範例，按一下 **[預覽]** 。  
  
10. 按一下 **[資料行]** 頁面，然後從 **[可用的輸入資料行]** 清單，拖曳至少一個資料行至 **[可用的查閱資料行]** 清單中的資料行。  
  
    > [!NOTE]  
    >  「查閱」轉換會自動對應具有相同名稱和相同資料類型的資料行。  
  
    > [!NOTE]  
    >  資料行必須具有要對應的相符資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。  
  
11. 執行下列工作，以便在輸出中包含查閱資料行：  
  
    1.  在 **[可用的查閱資料行]** 清單中。 選取資料行。  
  
    2.  在 **[查閱作業]** 清單中，指定查閱資料行的值要取代輸入資料行中的值，還是要寫入至新的資料行。  
  
12. 若要設定錯誤輸出，按一下 **[錯誤輸出]** 頁面，然後設定錯誤處理選項。 如需詳細資訊，請參閱[查閱轉換編輯器 &#40;錯誤輸出頁面&#41;](../lookup-transformation-editor-error-output-page.md)。  
  
13. 按一下 **[確定]** ，將變更儲存至查閱轉換，然後再執行封裝。  
  
## <a name="see-also"></a>另請參閱  
 [使用快取連線管理員以完整快取模式來實作查閱轉換](lookup-transformation-full-cache-mode-ole-db-connection-manager.md)   
 [以沒有快取或部分快取模式來實作查閱](../data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)   
 [Integration Services 轉換](../data-flow/transformations/integration-services-transformations.md)  
  
  
