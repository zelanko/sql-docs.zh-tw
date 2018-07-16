---
title: 建立共用資料集或內嵌資料集 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d1d7bc71-f0e9-4ce5-b3ad-6fee54388a31
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a3ba91c662bf925591d9a72d389c6a228d8b356e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192858"
---
# <a name="create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs"></a>建立共用資料集或內嵌資料集 (報表產生器及 SSRS)
  您可以建立內嵌資料集供單一報表使用，或建立要儲存到報表伺服器的共用資料集，以供多個報表使用。 若要建立資料集，您必須已經定義內嵌或共用資料來源。  
  
 請使用報表產生器來執行下列工作：  
  
-   在資料集設計檢視中建立共用資料集。 共用資料集必須使用已發行的共用資料來源。  
  
-   在報表設計檢視中建立內嵌資料集。  
  
-   將資料集直接儲存至報表伺服器或 SharePoint 網站。  
  
 請使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的報表設計師來執行下列工作：  
  
1.  在 [方案總管] 中建立共用資料集。 共用資料集必須使用 [方案總管] 中 [共用資料來源] 資料夾內的資料來源。  
  
2.  在 [報表資料] 窗格中建立內嵌資料集。  
  
3.  (選擇性) 使用報表來部署共用資料集和共用資料來源。 您可以針對每種項目類型，使用 [專案屬性] 來指定報表伺服器或 SharePoint 網站上資料夾的路徑。  
  
 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-open-report-builder-and-create-a-shared-dataset"></a>若要開啟報表產生器，並建立共用資料集  
  
1.  開啟報表產生器。 **[新增報表或資料集]** 窗格隨即開啟，如下圖所示：  
  
     ![rs_NewSharedDataset](../media/rs-newshareddataset.gif "rs_NewSharedDataset")  
  
    > [!NOTE]  
    >  如果 [New report or dataset pane (新增報表或資料集窗格)] 未出現，請從 [報表產生器] 按鈕按一下 [新增]。  
  
2.  在左窗格的 **[建立資料集]** 底下，按一下 **[共用資料集]**。  
  
3.  在右窗格中，按一下 **[瀏覽]** 從報表伺服器選取共用資料來源，然後按一下 **[建立]**。 隨即開啟與共用資料來源相關聯的查詢設計工具。  
  
4.  在查詢設計工具中，指定要併入資料集的欄位。  
  
5.  按一下 **「執行」** (**!**) 來執行查詢。  
  
6.  在 **[報表產生器]** 按鈕上，按一下 **[儲存]** 或 **[另存新檔]** ，將共用資料集儲存在報表伺服器上。  
  
7.  若要結束報表產生器，請按一下 **[報表產生器]**，然後按一下 **[結束報表產生器]**。 若要處理報表，按一下 **[報表產生器]**，然後按一下 **[新增]** 或 **[開啟]**。  
  
### <a name="to-set-query-parameter-options"></a>若要設定查詢參數選項  
  
1.  開啟報表產生器。  
  
2.  按一下 **[開啟]**。  
  
3.  瀏覽至報表伺服器，並選取共用資料來源的資料夾。  
  
4.  在 **[下列類型的項目]** 中，按一下下拉式清單中的資料集 (*.rsd)。  
  
5.  選取共用資料集，然後按一下 **[開啟]**。 隨即開啟關聯的查詢設計工具。  
  
6.  在功能區上，按一下 **[資料集屬性]**。  
  
7.  按一下 **[參數]**。 在這個頁面上，將預設值設定為常數或運算式，並將參數標示為唯讀、可為 Null 或 [從查詢中忽略]。 如需詳細資訊，請參閱[資料集屬性對話方塊、參數 &#40;報表產生器&#41;](../dataset-properties-dialog-box-parameters-report-builder.md)。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
### <a name="to-create-a-dataset-from-a-sql-server-relational-database"></a>若要從 SQL Server 關聯式資料庫建立資料集  
  
1.  在 [報表資料] 窗格中，以滑鼠右鍵按一下資料來源的名稱，然後按一下 **[加入資料集]**。 **[資料集屬性]** 對話方塊的 **[查詢]** 頁面隨即開啟。  
  
2.  在 **[名稱]** 中，輸入資料集名稱或是接受預設名稱。  
  
    > [!NOTE]  
    >  資料集名稱是在報表的內部使用。 為了清楚起見，我們建議資料集的名稱應該要描述查詢所傳回的資料。  
  
3.  在 **[資料來源]** 中，瀏覽並選取現有的共用資料來源名稱，或是按一下 **[新增]** 來建立新的內嵌資料來源。  
  
4.  選取 **[查詢類型]** 選項。 選項會因資料來源類型而異。  
  
    -   選取 **[Text]** ，即可使用資料來源的查詢語言來撰寫查詢。  
  
    -   選取 **[Table]** ，即可傳回關聯式資料庫資料表中的所有欄位。  
  
    -   選取 **[StoredProcedure]** 即可依名稱執行預存程序。  
  
5.  在 **[查詢]** 中，輸入查詢、預存程序或資料表名稱。 或者，您也可以按一下 **[查詢設計工具]** 來開啟圖形化或是以文字為基礎的查詢設計工具，或是按一下 **[匯入]** 從現有的報表匯入查詢。  
  
     在一些情況下，查詢所指定的欄位集合只能透過在資料來源上執行查詢來判斷。 例如，預存程序可能會在結果集中傳回一組變動的欄位。 按一下 **[重新整理欄位]** 可在資料來源上執行查詢，並擷取在 [報表資料] 窗格中填入資料集欄位集合所需的欄位名稱。 當您關閉 **[資料集屬性]** 對話方塊之後，資料集節點底下會出現欄位集合。  
  
6.  在 **[逾時]** 中，輸入報表伺服器等候資料庫回應的秒數。 預設值為 0 秒。 當逾時值為 0 秒時，此查詢不會逾時。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     資料集和它的欄位集合會出現在 [報表資料] 窗格的資料來源節點底下。  
  
## <a name="see-also"></a>另請參閱  
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)   
 [查詢設計工具 &#40;報表產生器&#41;](../query-designers-report-builder.md)   
 [對話方塊、窗格和精靈的報表產生器說明](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-datasets-ssrs.md)   
 [資料連接、 資料來源和報表產生器中的連接字串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [內嵌和共用資料集 &#40;報表產生器及 SSRS&#41;](embedded-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
