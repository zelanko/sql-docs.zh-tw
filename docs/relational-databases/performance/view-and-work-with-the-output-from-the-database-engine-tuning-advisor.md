---
title: "檢視及處理 Database Engine Tuning Advisor 的輸出 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dta.sessionmonitor.f1
- sql13.dta.reports.f1
- sql13.dta.recommendations.f1
- sql13.dta.applyrecommendations.f1
helpviewer_keywords:
- viewing logs
- recommendations [Database Engine Tuning Advisor]
- summary tuning information [SQL Server]
- Database Engine Tuning Advisor [SQL Server], recommendations
- Database Engine Tuning Advisor [SQL Server], logs
- Database Engine Tuning Advisor [SQL Server], viewing output
- Database Engine Tuning Advisor [SQL Server], reports
- logs [SQL Server], tuning
- reports [SQL Server], tuning
- viewing tuning output
ms.assetid: 47f9d9a7-80b0-416d-9d9a-9e265bc190dc
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ce827e3df11e103bced1b62afb2329db9c81e0f4
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="view-and-work-with-the-output-from-the-database-engine-tuning-advisor"></a>檢視及處理 Database Engine Tuning Advisor 的輸出
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Database Engine Tuning Advisor 微調資料庫時，會建立摘要、建議、報表和微調記錄。 您可以使用微調記錄輸出針對 Database Engine Tuning Advisor 的微調工作階段進行疑難排解。 您可以使用摘要、建議和報表來判定是否要實作微調建議，或繼續微調，直到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝的查詢效能改進達到所需的程度為止。 如需有關如何使用 Database Engine Tuning Advisor 來建立工作負載及微調資料庫的詳細資訊，請參閱＜ [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)＞。  
  
##  <a name="View"></a> 檢視微調輸出  
 下列程序描述如何使用 Database Engine Tuning Advisor GUI 來檢視微調建議、摘要、報表和微調記錄。 如需有關使用者介面選項的詳細資訊，請參閱本主題稍後的＜ [使用者介面描述](#UI) ＞。  
  
 您也可以使用 GUI 來檢視由 **dta** 命令列公用程式產生的微調輸出。  
  
> [!NOTE]  
>  如果您使用 **dta** 命令列公用程式並指定以 **-ox** 引數將輸出寫入到 XML 檔案，則在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的 [檔案] 功能表上按一下 [開啟檔案]，即可開啟並檢視 XML 輸出檔。 如需詳細資訊，請參閱 [Use SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)。 如需 **dta** 命令列公用程式的相關資訊，請參閱 [dta 公用程式](../../tools/dta/dta-utility.md)。  
  
#### <a name="to-view-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>以 Database Engine Tuning Advisor GUI 檢視微調建議  
  
1.  使用 Database Engine Tuning Advisor GUI 或 **dta** 命令列公用程式微調資料庫。 如需詳細資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。 如果您要使用現有的微調工作階段，請略過這個步驟，繼續執行步驟 2。  
  
2.  開始 Database Engine Tuning Advisor GUI。 如需詳細資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。 若要檢視現有微調工作階段的微調建議，請按兩下 [工作階段監視器] 視窗中的工作階段名稱來開啟。  
  
     在新的微調工作階段完成之後，或在工具載入現有的工作階段後，會顯示 **[建議]** 頁面。  
  
3.  在 **[建議]** 頁面上，請按一下 **[資料分割建議]** 和 **[索引建議]** ，來檢視顯示微調工作階段結果的窗格。 如果在設定此工作階段的微調選項時沒有指定資料分割，則 **[資料分割建議]** 窗格會是空的。  
  
4.  在 **[資料分割建議]** 或 **[索引建議]** 窗格中，請使用捲軸來檢視方格中顯示的所有資訊。  
  
5.  取消選取 **[建議]** 索引標籤式頁面底部的 **[顯示現有的物件]** 。 這會讓方格只顯示建議中所參考的那些資料庫物件。 使用底部的捲軸來檢視建議方格中最右邊的欄位，然後按一下 [定義] 欄位中的一個項目，來檢視或複製會在資料庫中建立該物件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。  
  
6.  如果您要將所有會建立或卸除此項建議中所有資料庫物件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼儲存到一個指令碼檔案中，請按一下 **[動作]** 功能表上的 **[儲存建議]** 。  
  
#### <a name="to-view-the-tuning-summary-and-reports-with-the-database-engine-tuning-advisor-gui"></a>若要以 Database Engine Tuning Advisor GUI 檢視微調摘要和報表  
  
1.  使用 Database Engine Tuning Advisor GUI 或 **dta** 命令列公用程式微調資料庫。 如需詳細資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。 如果您要使用現有的微調工作階段，請略過這個步驟，繼續執行步驟 2。  
  
2.  開始 Database Engine Tuning Advisor GUI。 如需詳細資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。 若要檢視現有微調工作階段的微調摘要和報表，請按兩下 [工作階段監視器] 中的工作階段名稱來開啟。  
  
3.  在新的微調工作階段完成之後，或在工具載入現有的工作階段後，請按一下 **[報表]** 索引標籤。  
  
4.  **[微調摘要]** 窗格包含微調工作階段的相關資訊。 由 **[預期的改進百分比]** 和 **[建議使用的空間]** 項目所提供的資訊，對於您決定是否要實作建議特別有用。  
  
5.  在 **[微調報表]** 窗格中，按一下 **[選取報表]** 來選擇要檢視的微調報表。  
  
#### <a name="to-view-tuning-logs-with-the-database-engine-tuning-advisor-gui"></a>若要以 Database Engine Tuning Advisor GUI 檢視微調記錄  
  
1.  使用 Database Engine Tuning Advisor GUI 或 **dta** 命令列公用程式微調資料庫。 微調工作負載時請確定您已勾選 **[一般]** 索引標籤上的 **[儲存微調記錄]** 。 如果您要使用現有的微調工作階段，請略過這個步驟，繼續執行步驟 2。  
  
2.  開始 Database Engine Tuning Advisor GUI。 如需詳細資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。 若要檢視現有微調工作階段的微調摘要與報告，請按兩下 [工作階段監視器] 視窗中的工作階段名稱來開啟。  
  
3.  在新的微調工作階段完成之後，或在工具已經載入現有的工作階段後，請按一下 **[進度]** 索引標籤。 **[微調記錄]** 窗格會顯示記錄的內容。 此記錄包含 Database Engine Tuning Advisor 無法分析的工作負載事件之相關資訊。  
  
     如果 Database Engine Tuning Advisor 已經分析過微調工作階段中的所有事件，則會顯示訊息指出該工作階段的微調記錄是空的。 若當初執行微調工作階段時並未勾選 **[一般]** 索引標籤上的 **[儲存微調記錄]** ，系統會顯示訊息指出此問題。  
  
##  <a name="Implement"></a> 實作微調建議  
 您可以手動實作 Database Engine Tuning Advisor 建議，或是作為微調工作階段的一部份自動實作。 如果實作前想要先檢查微調結果，請使用 Database Engine Tuning Advisor GUI。 然後您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來手動執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼，這些指令碼是 Database Engine Tuning Advisor 分析實作建議的工作負載而產生。 如果在實作前不需要檢查結果，可將 **-a** 選項與 **dta** 命令提示字元公用程式一起使用。 這會導致公用程式在分析工作負載後自動執行微調建議。 下列程序解釋如何使用兩種 Database Engine Tuning Advisor 介面，實作微調建議。  
  
#### <a name="to-manually-implement-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>若要使用 Database Engine Tuning Advisor GUI 手動實作微調建議  
  
1.  使用 Database Engine Tuning Advisor GUI 或 **dta** 命令提示字元公用程式微調資料庫。 如需詳細資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。 如果您要使用現有的微調工作階段，請略過這個步驟，繼續執行步驟 2。  
  
2.  開始 Database Engine Tuning Advisor GUI。 如需詳細資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。 如果想要實作現有微調工作階段的微調建議，請按兩下 [工作階段監視器] 中的工作階段名稱開啟它。  
  
3.  在新的微調工作階段結束後，或在工具載入現有的工作階段後，在 **[動作]** 功能表上，按一下 **[套用建議事項]** 。  
  
4.  在 **[套用建議事項]** 對話方塊中，選擇 **[立即套用]** 或 **[排程在稍後執行]**。 如果選擇 **[排程在稍後執行]**，請選取適當的日期和時間。  
  
5.  按一下 **[確定]** 以套用建議事項。  
  
#### <a name="to-automatically-implement-tuning-recommendations-using-the-dta-command-prompt-utility"></a>若要使用 dta 命令提示字元公用程式自動實作微調建議  
  
1.  決定您希望 Database Engine Tuning Advisor 在分析過程中考慮加入、移除或保留的資料庫功能 (索引、索引檢視、分割)。  
  
     開始進行微調之前，請記住下列考量：  
  
    -   使用追蹤資料表做為工作負載時，該資料表必須位於 Database Engine Tuning Advisor 所微調的同一部伺服器上。 如果在另外的伺服器上建立追蹤資料表，請將它移動到 Database Engine Tuning Advisor 正在進行微調的伺服器。  
  
    -   如果微調工作階段持續執行的時間長度超過預期，則可以按下 CTRL+C，結束該微調工作階段。 在這些情況下按 CTRL+C 可強制 **dta** 根據其可承擔的工作負載，產生可行的最佳建議，而不會浪費工具用來微調工作負載的時間。  
  
2.  從命令提示字元，輸入下列內容：  
  
    ```  
    dta -E -D DatabaseName -if WorkloadFile -s SessionName -a  
    ```  
  
     其中 **-E** 可指定微調工作階段使用信任連接 (而非登入識別碼與密碼)； **-D** 可指定想要微調的資料庫名稱，或工作負載會用到的多個資料庫清單 (以逗號分隔)； **-if** 可指定工作負載檔案的名稱與路徑； **-s** 可指定微調工作階段的名稱，而 **-a** 則指定要讓 **dta** 命令提示字元公用程式在分析過工作負載後，不需提示就自動套用微調建議。 如需有關使用 **dta** 命令提示字元公用程式微調資料庫的詳細資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。  
  
3.  按 ENTER 鍵。  
  
##  <a name="Analysis"></a> 執行探勘分析  
 Database Engine Tuning Advisor 有一項由使用者指定的組態功能，可讓資料庫管理員執行探勘分析。 資料庫管理員可以使用此功能，將所需的實體資料庫設計指定給 Database Engine Tuning Advisor，並可在不實作的情況下，評估該設計的效能。 Database Engine Tuning Advisor 圖形使用者介面 (GUI) 及命令列公用程式皆可支援使用者指定的組態。 不過，命令列公用程式提供的彈性最大。  
  
 若您使用 Database Engine Tuning Advisor GUI，您可以評估實作 Database Engine Tuning Advisor 微調建議子集的效果，但您不能加入假設性的實體設計結構來供 Database Engine Tuning Advisor 評估。  
  
 下列程序說明如何以這二種工具介面來應用使用者指定的組態功能。  
  
### <a name="using-database-engine-tuning-advisor-gui-to-evaluate-tuning-recommendations"></a>使用 Database Engine Tuning Advisor GUI 來評估微調建議  
 下列程序說明如何評估 Database Engine Tuning Advisor 所產生的建議，但是 GUI 不能讓您指定新的實體設計結構以供評估。  
  
##### <a name="to-evaluate-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>若要以 Database Engine Tuning Advisor GUI 評估微調建議  
  
1.  請使用 Database Engine Tuning Advisor 圖形使用者介面 (GUI) 來微調資料庫。 如需詳細資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。 若您想要評估現有的微調工作階段，請在 [工作階段監視器] 中按兩下該工作階段。  
  
2.  在 **[建議]** 索引標籤上，清除您不想使用的建議實體設計結構。  
  
3.  在 **[動作]** 功能表上，按一下 **[評估建議]**。 就會為您建立新的微調工作階段。  
  
4.  輸入新的 **[工作階段名稱]**。 若要檢視您所評估的實體資料庫設計結構組態，請在 Database Engine Tuning Advisor 應用程式視窗底部的 **[描述]** 區域中，選擇 **[按一下此處以查看組態區段]** 。  
  
5.  按一下工具列上的 **[開始分析]** 按鈕。 Database Engine Tuning Advisor 完成時，您可以在 **[建議]** 索引標籤上檢視結果。  
  
### <a name="using-database-engine-tuning-advisor-gui-to-export-tuning-session-results-for-what-if-tuning-analysis"></a>使用 Database Engine Tuning Advisor GUI 匯出微調工作階段結果，以進行假設微調分析  
 下列程序說明如何將 Database Engine Tuning Advisor 微調工作階段結果匯出至 XML 檔案，您可以編輯此檔案，然後以 **dta** 命令列公用程式加以微調。 您可利用此程序針對假設的新款實際設計結構，執行微調分析，而不必在您找出結構是否可產生所需的效能改善之前，將其實作於資料庫中而造成負擔。 對於不熟悉 XML 的使用者來說，若想利用 Database Engine Tuning Advisor XML 結構描述的彈性來執行模擬分析，使用 Database Engine Tuning Advisor GUI 先初步微調資料庫，然後再將微調結果匯出至 **.xml** 檔案，這個方法會很好用。  
  
##### <a name="to-export-tuning-session-results-from-the-database-engine-tuning-advisor-gui-for-what-if-analysis-with-the-dta-command-line-utility"></a>若要從 Database Engine Tuning Advisor GUI 匯出微調工作階段結果，以使用 dta 命令列公用程式來進行假設分析  
  
1.  請使用 Database Engine Tuning Advisor 圖形使用者介面 (GUI) 來微調資料庫。 如需詳細資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。 若您想要評估現有的微調工作階段，請在 [工作階段監視器] 中按兩下該工作階段。  
  
2.  在 **[檔案]** 功能表上，按一下 **[匯出工作階段結果]** ，並儲存成 XML 檔案。  
  
3.  在您喜好的 XML 編輯器、文字編輯器或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟步驟 2 中建立的 XML 檔案。 向下捲動至 **Configuration** 元素。 將 **Configuration** 元素區段複製並貼到 XML 輸入檔範本中的 **TuningOptions** 元素之後。 儲存此 XML 輸入檔。  
  
4.  在步驟 3 所建立的新 XML 輸入檔中，於 **TuningOptions** 元素中指定您所需的任何微調選項、編輯 **Configuration** 元素區段 (依您的分析需求來新增或刪除實體設計結構)、儲存檔案，然後以 Database Engine Tuning Advisor XML 結構描述來加以驗證。 如需編輯此 XML 檔案的資訊，請參閱 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)。  
  
5.  使用步驟 4 中所建立的 XML 檔案，作為 **dta** 命令列公用程式的輸入檔。 如需有關 XML 輸入檔與此工具一起使用的詳細資訊，請參閱＜ [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)＞中的＜使用 dta 公用程式微調資料庫＞。  
  
### <a name="using-the-user-specified-configuration-feature-with-the-dta-command-line-utility"></a>以 dta 命令列公用程式來應用使用者指定的組態功能  
 若您是有經驗的 XML 開發人員，您可以建立 Database Engine Tuning Advisor XML 輸入檔，在檔案中指定工作負載及實際資料庫設計結構的假設組態，例如：索引、索引檢視或資料分割。 然後您可以使用 **dta** 命令列公用程式，分析此假設組態對資料庫之查詢效能的影響。 下列程序將逐步說明這項處理：  
  
##### <a name="to-use-the-user-specified-configuration-feature-with-the-dta-command-line-utility"></a>若要以 dta 命令列公用程式來應用使用者指定的組態功能  
  
1.  建立微調工作負載。 如需有關執行此工作的資訊，請參閱＜ [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)＞。  
  
2.  將[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md) 複製並貼到您的 XML 編輯器或文字編輯器中。 使用此範例來為您的微調工作階段建立 XML 輸入檔。 如需有關執行此工作的詳細資訊，請參閱＜ [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)＞中的＜建立 XML 輸入檔案＞一節。  
  
3.  編輯範例 XML 輸入檔中的 **TuningOptions** 及 **Configuration** 元素。 在 **TuningOptions** 元素中，指定您要讓 Database Engine Tuning Advisor 在微調工作階段納入考量的實體設計結構。 在 **Configuration** 元素中指定實體設計結構，該結構需符合您要 Database Engine Tuning Advisor 分析之實體資料庫設計結構的假設組態。 若想知道您可以將哪些屬性及子元素用於 **TuningOptions** 和 **Configuration** 父元素，請參閱 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)。  
  
4.  請用 **.xml** 副檔名來儲存輸入檔。  
  
5.  用 Database Engine Tuning Advisor XML 結構描述來驗證您在步驟 4 中儲存的 XML 輸入檔。 當您安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，此結構描述會安裝在下列位置：  
  
    ```  
    C:\Program Files\Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd  
    ```  
  
     您也可以自線上取得 Database Engine Tuning Advisor XML 結構描述： [http://schemas.microsoft.com/sqlserver/2004/07/dta](http://schemas.microsoft.com/sqlserver/2004/07/dta)。  
  
6.  建立工作負載及 XML 輸入檔之後，即可準備將輸入檔提交至 **dta** 命令列公用程式，以進行分析。 請確定您有指定 **-ox** 公用程式引數的 XML 輸出檔名稱。 這樣會以 **Configuration** 元素中所指定的建議組態來建立 XML 輸出檔。 若您想再執行一次 Database Engine Tuning Advisor，以檢查另一個以該輸出檔為基礎的假設組態，則您可以複製輸出檔的 **Configuration** 元素內容，並貼到新的 XML 輸入檔或原來的 XML 輸入檔中。 如需有關 XML 輸入檔與 **dta** 公用程式一起使用的資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)中的＜使用 dta 公用程式微調資料庫＞。  
  
     微調完成後，您可以使用 Database Engine Tuning Advisor GUI 來檢視微調報表，也可以開啟 XML 輸出檔來檢視 **TuningSummary** 和 **Configuration** 元素，以檢視 Database Engine Tuning Advisor 的建議。 如需有關檢視微調工作階段結果的詳細資訊，請參閱本主題前面的＜ [檢視微調輸出](#View) ＞。 另請注意，XML 輸出檔可能含有 Database Engine Tuning Advisor 分析報表。  
  
7.  重複步驟 6 及 7，直到您建立的假設組態可產生出您所需的查詢效能改善。 然後您就可以實作這個新的組態。 如需詳細資訊，請參閱本主題前面的＜ [實作微調建議](#Implement) ＞。  
  
##  <a name="ReviewEvaluateClone"></a> 檢閱、評估及複製微調工作階段  
 每次當您開始分析一或多個資料庫上的工作負載影響時，Database Engine Tuning Advisor 都會建立新的微調工作階段。 您可以使用 Database Engine Tuning Advisor GUI 的 **[工作階段監視器]** 來檢視或重新載入在特定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上執行的所有微調工作階段。 讓所有現有的微調工作階段都可供檢視，您就可以輕鬆地：根據現有工作階段來複製工作階段、編輯現有的微調建議，然後使用 Database Engine Tuning Advisor 來評估已編輯的工作階段，或定期執行微調以監視資料庫的實際設計。 例如，您可以決定以每月排程來微調資料庫。  
  
 檢閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的任何微調工作階段前，您必須使用 Database Engine Tuning Advisor 來微調工作負載，以在伺服器執行個體上建立微調工作階段。 如需詳細資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。  
  
### <a name="review-existing-tuning-sessions"></a>檢閱現有的微調工作階段  
 使用下列步驟來瀏覽特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上的現有微調工作階段。  
  
##### <a name="to-review-existing-tuning-sessions"></a>若要檢閱現有的微調工作階段  
  
1.  開始 Database Engine Tuning Advisor GUI。 如需詳細資訊，請參閱 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。  
  
2.  現有的微調工作階段會顯示在 **[工作階段監視器]** 視窗的上半部。 顯示的工作階段數目視您已在此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上執行的資料庫微調次數而定。 使用捲軸來檢視所有微調工作階段。  
  
3.  按一下微調工作階段名稱，其詳細資料就會出現在 **[工作階段監視器]** 視窗的下半部。  
  
4.  按兩下微調工作階段名稱，其資訊就會載入到 Database Engine Tuning Advisor。 載入工作階段資訊後，您可以選擇其中任何一個索引標籤來檢視此微調工作階段的相關資訊。  
  
### <a name="evaluate-existing-tuning-sessions-as-hypothetical-configurations"></a>以假設組態評估現有的微調工作階段  
 使用下列步驟來評估現有的微調工作階段。 評估現有的微調工作階段牽涉到檢視與編輯其建議，然後重新微調。 例如，您決定只要在 **table1**上建立索引，您從現有的微調建議中刪除索引檢視與分割。 接著，Database Engine Tuning Advisor 會建立新的微調工作階段，並使用已編輯的建議作為假設組態，來微調您資料庫的工作負載。 這表示 Database Engine Tuning Advisor 會微調資料庫的工作負載 (就如同已實作編輯後的建議)，讓您可以執行有限的假設條件分析。 稱之為有限的假設條件分析的原因是，當您使用 Database Engine Tuning Advisor GUI 時只能選擇現有建議的子集。 若要執行完整的模擬分析，您必須指定全新的假設組態 (此組態不能是任何先前微調工作階段的子集)，您必須使用 Database Engine Tuning Advisor XML 輸入檔來搭配 **dta** 命令列公用程式。  
  
##### <a name="to-evaluate-an-existing-tuning-session"></a>若要評估現有的微調工作階段  
  
1.  啟動 Database Engine Tuning Advisor 之後，在 [工作階段監視器] 上半部的微調工作階段按兩下，將工作階段資訊載入至 Database Engine Tuning Advisor。  
  
2.  按一下 **[進度]** 索引標籤來檢查微調記錄，其中包含 Database Engine Tuning Advisor 無法微調之工作負載中任何事件的相關錯誤資訊。 此資訊可協助您評估工作負載的效能。  
  
3.  若要進一步檢閱此工作階段的微調結果，請按一下 **[報表]** 索引標籤。 在該索引標籤中，您可以檢視微調摘要，或從 **[選取報表]** 清單中選擇微調報表。  
  
4.  按一下 **[建議]** 索引標籤以檢視微調建議。  
  
5.  若對於實作建議有任何不確定，請取消核取。  
  
6.  在 **[動作]** 功能表上，按一下 **[評估建議]**。 Database Engine Tuning Advisor 會建立使用已編輯建議作為假設組態的新微調工作階段。 若要以 XML 檢視假設組態，請選擇 **[按一下此處以查看組態區段]**。  
  
7.  在 **[一般]** 索引標籤上，輸入 **工作階段名稱**，並且確保已指定正確的 **[工作負載]** 。  
  
8.  在 **[微調選項]** 索引標籤上，您可以指定微調時間或任何 **[進階選項]**。  
  
9. 按一下工具列上的 **[開始分析]** 按鈕。 Database Engine Tuning Advisor 會使用假設組態開始微調資料庫。 當 Database Engine Tuning Advisor 完成時，您可以就像平常對於任何工作階段一樣的檢視這個工作階段的結果。  
  
### <a name="clone-existing-tuning-sessions"></a>複製現有的微調工作階段  
 您可以選擇 Database Engine Tuning Advisor 中的複製選項，以根據現有的工作階段來建立新的微調工作階段。 使用複製選項時，您是以現有的工作階段為基礎來建立新的微調工作階段。 接著，您可以視需要變更新工作階段的微調選項。 如前述步驟所述評估現有的工作階段時，Database Engine Tuning Advisor 也會建立新的微調工作階段，但您無法變更微調選項。  
  
##### <a name="to-create-new-tuning-sessions-by-cloning-existing-sessions"></a>藉由複製現有的工作階段來建立新的微調工作階段  
  
1.  啟動 Database Engine Tuning Advisor 之後，在 [工作階段監視器] 上半部的微調工作階段按兩下，將工作階段資訊載入至 Database Engine Tuning Advisor。  
  
2.  在 **[動作]** 功能表上，按一下 **[複製工作階段]**。  
  
3.  在 **[一般]** 索引標籤上，輸入 **工作階段名稱**，並且確保已指定正確的 **[工作負載]** 。  
  
4.  在 **[微調選項]** 索引標籤上，您可以指定微調時間，Database Engine Tuning Advisor 應該考慮建立的實體設計結構，以及考慮應該在其建議中卸除的項目。  
  
5.  若要在 **上線時設定建議的空間限制、每個索引的資料行數上限，以及是否要讓 Database Engine Tuning Advisor 產生可實作的建議，請按一下** [進階選項] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
6.  按一下工具列上的 **[開始分析]** 按鈕，如同其他微調工作階段一樣分析工作負載的效果。 當 Database Engine Tuning Advisor 完成時，您可以就像平常對於任何工作階段一樣的檢視這個工作階段的結果。  
  
##  <a name="UI"></a> 使用者介面描述  
  
### <a name="sessions-monitor"></a>工作階段監視器  
 **[工作階段監視器]** 會顯示有關 Database Engine Tuning Advisor 中已開啟之工作階段的資訊。 若要顯示屬性視窗中有關工作階段的資訊，請在 **[工作階段監視器]**中選取工作階段名稱。  
  
### <a name="recommendations-tab"></a>建議索引標籤  
 Database Engine Tuning Advisor 完成工作負載分析後，即顯示 **[建議]** 索引標籤。 此方格包含各考量物件的建議。 如果有資料分割建議，則會出現在上方格，而索引建議會出現在下方格。 如果沒有建議就不會出現方格。  
  
 **[定義]** 資料行包含建議的資料分割或索引的定義，並以超連結方式顯示。 此資料行通常太窄，無法看到整個定義。 按一下超連結以顯示包含完整定義與 **[複製至剪貼簿]** 按鈕的對話方塊。  
  
#### <a name="partition-recommendations"></a>[資料分割建議]  
 **資料庫名稱**  
 資料庫包含建議要修改的物件。  
  
 **建議**  
 提升效能的建議動作。 可能的值為 Create 和 Drop。  
  
 **建議的目標**  
 受建議影響的資料分割函數或配置。 此資料行的圖示反映要卸除或加入 **[建議的目標]** 的建議，以及是否為資料分割函數或配置。  
  
 **詳細資料**  
 [建議的目標] 的描述。 可能的值包括資料分割函數的範圍，或資料分割配置為空白。  
  
 [資料分割的數目]****  
 由建議的資料分割函數所定義之資料分割的數目。 此函數與配置一起使用，並套用至資料表時，資料表中的資料就會劃分為多個資料分割。  
  
 **[定義]**  
 [建議的目標] 的定義。 按一下資料行，即可開啟包含建議動作之指令碼的 [SQL 指令碼預覽] 對話方塊。  
  
##### <a name="index-recommendations"></a>[索引建議]  
 **資料庫名稱**  
 資料庫包含建議要修改的物件。  
  
 **Object Name**  
 與建議相關的資料表。  
  
 **建議**  
 提升效能的建議動作。 可能的值為 Create 和 Drop。  
  
 **建議的目標**  
 受建議影響的索引或檢視。 此資料行的圖示反映要卸除或加入 **[建議的目標]**的建議。  
  
 **詳細資料**  
 [建議的目標] 的描述。 可能的值包括叢集、索引檢視或代表非叢集索引的空白。 此外還指出索引是否是唯一的。  
  
 **資料分割配置**  
 如果建議資料分割，則會在此資料行中提供資料分割配置。  
  
 **大小 (KB)**  
 建議的新物件的預期大小。 如果此資料行是空白，請按一下 **[請參閱報表，以取得現有物件的大小]**。  
  
 **[定義]**  
 [建議的目標] 的定義。 按一下資料行，即可開啟包含建議動作之指令碼的 [SQL 指令碼預覽] 對話方塊。  
  
 **[建議]**  
 選取即可在方格中顯示所有現有的物件，即使 Database Engine Tuning Advisor 沒有與物件相關的建議亦同。  
  
 **[請參閱報表，以取得現有物件的大小]**  
 選取即可檢視報表，此報表在建議方格中提供現有物件的大小。  
  
### <a name="actions-menuapply-recommendations-options"></a>動作功能表/應用建議選項  
 在分析了工作負載以及提出了建議之後，請在 **[動作]** 功能表上按一下 **[套用建議]** ，來開啟 **[套用建議]** 對話方塊。  
  
 **[立即套用]**  
 產生建議的指令碼，並執行該指令碼以實作建議。  
  
 **[排程在稍後執行]**  
 產生建議的指令碼，並將動作儲存為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。  
  
 **日期**  
 指定您想要執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業以套用建議的日期。  
  
 **Time**  
 指定您想要執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業以套用建議的時間。  
  
### <a name="reports-tab-options"></a>報表索引標籤選項  
 Database Engine Tuning Advisor 完成工作負載的分析後，就會出現 **[報表]** 索引標籤。  
  
 **[微調摘要]**  
 顯示 Database Engine Tuning Advisor 建議的摘要。  
  
 **日期**  
 Database Engine Tuning Advisor 建立報表的日期。  
  
 **Time**  
 Database Engine Tuning Advisor 建立報表的時間。  
  
 **Server**  
 Database Engine Tuning Advisor 工作負載的目標伺服器。  
  
 **要微調的資料庫**  
 受 Database Engine Tuning Advisor 建議影響的資料庫。  
  
 **工作負載檔案**  
 工作負載為檔案時顯示。  
  
 **工作負載資料表**  
 工作負載為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表時顯示。  
  
 **[工作負載]**  
 工作負載從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的查詢編輯器中匯入時顯示。  
  
 **最大微調時間**  
 設定 Database Engine Tuning Advisor 分析時可用的最大時間。  
  
 **微調花費的時間**  
 Database Engine Tuning Advisor 實際用來分析工作負載的時間。  
  
 **[預期的改進百分比]**  
 如果實作所有 Database Engine Tuning Advisor 建議，目標工作負載所預期的改進百分比。  
  
 **建議的最大空間 (MB)**  
 建議考慮使用的最大空間。 此值必須在分析之前設定，請使用 **[微調選項]** 索引標籤上的 **[進階選項]** 按鈕。  
  
 **目前使用的空間 (MB)**  
 在已分析資料庫中目前索引正在使用的空間。  
  
 **建議使用的空間 (MB)**  
 如果實作所有 Database Engine Tuning Advisor 建議，預期索引會使用的近似空間。  
  
 **工作負載中的事件數目**  
 工作負載中包含的事件數目。  
  
 **微調的事件數目**  
 工作負載中已微調的事件數目。 如果無法微調事件，則事件會列於微調記錄檔內的 **[進度]** 索引標籤。  
  
 **微調的陳述式數目**  
 工作負載中已微調的陳述式數目。 如果無法微調陳述式，則陳述式會列於微調記錄檔內的 **[進度]** 索引標籤。  
  
 **微調集內的 SELECT 陳述式百分比**  
 屬於 SELECT 陳述式的微調陳述式百分比。 只有在 SELECT 陳述式已微調後才會顯示。  
  
 **微調集內的 UPDATE 陳述式百分比**  
 屬於 UPDATE 陳述式的微調陳述式百分比。 只有在 UPDATE 陳述式已微調後才會顯示。  
  
 **建議要 [建立 | 卸除] 的索引數目**  
 建議要在微調資料庫中建立或卸除的索引數目。 只有在索引屬於建議的一部份時才會顯示。  
  
 **建議要 [建立 | 卸除] 之檢視上的索引數目**  
 建議要在微調資料庫中建立或卸除之檢視上的索引數目。 只有在檢視上的索引屬於建議的一部份時才會顯示。  
  
 **建議要建立的統計資料數目**  
 建議要在微調資料庫中建立的統計資料數目。 只有在建議統計資料時才會顯示。  
  
 **Select Report**  
 查看選取之報表的詳細資料。 各報表的方格資料行有所差異。  
  
## <a name="see-also"></a>另請參閱  
 [Start and Use the Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [dta 公用程式](../../tools/dta/dta-utility.md)  
  
  
