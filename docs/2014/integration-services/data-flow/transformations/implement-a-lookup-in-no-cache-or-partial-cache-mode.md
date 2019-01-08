---
title: 以沒有快取或部分快取模式實作查閱 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: 01b7fbca-5181-4d47-9f75-7f25af6b40d2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fb778827f9193cd9fae136e078e353241d2b55ae
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52769740"
---
# <a name="implement-a-lookup-in-no-cache-or-partial-cache-mode"></a>以沒有快取或部分快取模式實作查閱
  您可以將查閱轉換設定為使用部分快取或沒有快取模式：  
  
-   部分快取  
  
     在參考資料集中具有相符項目的資料列，以及在資料集中沒有相符項目的資料列 (選擇性)，都會儲存在快取中。 超過快取的記憶體大小時，查閱轉換會自動從快取中移除最不常用的資料列。  
  
-   沒有快取  
  
     沒有資料會載入到快取。  
  
 不論是選取部份快取或沒有快取，都是使用 OLE DB 連接管理員連接到參考資料集。 參考資料集是藉由在執行查閱轉換期間使用資料表、檢視或 SQL 查詢而產生。  
  
### <a name="to-implement-a-lookup-transformation-in-no-cache-or-partial-cache-mode"></a>若要以沒有快取或部分快取模式實作查閱轉換  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，開啟包含所要封裝的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 專案，然後再開啟封裝。  
  
2.  在 **[資料流程]** 索引標籤上，加入查閱轉換。  
  
3.  從來源或先前的轉換將連接子拖曳到查閱轉換，以便將查閱轉換連接到資料流程。  
  
    > [!NOTE]  
    >  設定為使用無快取模式的查閱轉換如果連接到包含空白日期欄位的一般檔案，則查閱轉換可能不會驗證。 此轉換是否會驗證將取決於一般檔案的連線管理員是否已設定為保留 null 值。 若要確保查閱轉換會驗證，請在 **[一般檔案來源編輯器]** 的 **[連線管理員]** 頁面上，選取 **[將來源的 Null 值保留為資料流程中的 Null 值]** 選項。  
  
4.  按兩下來源或前一個轉換以設定元件。  
  
5.  按兩下 [查閱轉換]，然後在 [查閱轉換編輯器] 的 [一般] 頁面上，選取 [部分快取] 或 [無快取]。  
  
6.  針對 **[指定如何處理無相符項目的資料列]** 清單，選取清單中的錯誤處理選項。  
  
7.  在 **[連接]** 頁面上，從 **[OLE DB 連接管理員]** 清單選取連接管理員，或按一下 **[新增]** 建立新的連接管理員。 如需相關資訊，請參閱 [OLE DB Connection Manager](../../connection-manager/ole-db-connection-manager.md)。  
  
8.  執行下列其中一個步驟：  
  
    -   按一下 **[使用資料表或檢視]**，然後選取資料表或檢視，或按一下 **[新增]** 建立資料表或檢視。  
  
    -   按一下 **[使用 SQL 查詢的結果]**，然後在 **[SQL 命令]** 視窗中建立查詢。  
  
         -或-  
  
         按一下 **[建立查詢]** ，即可使用 **[查詢產生器]** 提供的圖形工具建立查詢。  
  
         -或-  
  
         按一下 **[瀏覽]** ，從檔案匯入 SQL 陳述式。  
  
     若要驗證 SQL 查詢，請按一下 **[剖析查詢]**。  
  
     若要檢視資料範例，按一下 **[預覽]**。  
  
9. 按一下 **[資料行]** 頁面，然後從 **[可用的輸入資料行]** 清單，拖曳至少一個資料行至 **[可用的查閱資料行]** 清單中的資料行。  
  
    > [!NOTE]  
    >  「查閱」轉換會自動對應具有相同名稱和相同資料類型的資料行。  
  
    > [!NOTE]  
    >  資料行必須具有要對應的相符資料類型。 如需詳細資訊，請參閱 [Integration Services Data Types](../integration-services-data-types.md)。  
  
10. 執行下列步驟，在輸出中包含查閱資料行：  
  
    1.  從 **[可用的查閱資料行]** 清單選取資料行。  
  
    2.  在 **[查閱作業]** 清單中，指定查閱資料行的值要取代輸入資料行中的值，還是要寫入至新的資料行。  
  
11. 如果在步驟 5 中選取的是 **[部分快取]** ，請在 **[進階]** 頁面上設定下列快取選項：  
  
    -   從 [快取大小 (32 位元)] 清單選取 32 位元環境的快取大小。  
  
    -   從 [快取大小 (64 位元)] 清單選取 64 位元環境的快取大小。  
  
    -   若要快取在參考中沒有相符項目的資料列，請選取 **[針對無相符項目的資料列啟用快取]**。  
  
    -   從 **[來自快取的配置]** 清單，選取要用來儲存沒有相符項目的資料列的快取百分比。  
  
12. 若要修改產生參考資料集的 SQL 陳述式，選取 **[修改 SQL 陳述式]**，然後變更顯示在文字方塊中的 SQL 陳述式。  
  
     如果陳述式包含參數，請按一下 **[參數]** 以將參數對應至輸入資料行。  
  
    > [!NOTE]  
    >  在此頁面上所指定的選擇性 SQL 陳述式會覆寫並取代在 [查閱轉換編輯器] 的 [連接]頁面上所指定的資料表名稱。  
  
13. 若要設定錯誤輸出，按一下 **[錯誤輸出]** 頁面，然後設定錯誤處理選項。 如需詳細資訊，請參閱[查閱轉換編輯器 &#40;錯誤輸出頁面&#41;](../../lookup-transformation-editor-error-output-page.md)。  
  
14. 按一下 **[確定]** ，將變更儲存至查閱轉換，然後再執行封裝。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 轉換](integration-services-transformations.md)  
  
  
