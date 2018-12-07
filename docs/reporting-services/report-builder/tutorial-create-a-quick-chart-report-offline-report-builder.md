---
title: 教學課程：離線建立快速圖表報表 (報表產生器) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
helpviewer_keywords:
- reports, creating
- tutorials, getting started
- creating reports
ms.assetid: 6b1db67a-cf75-494c-b70c-09f1e6a8d414
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bfb9b14f518b20cd318cd6a532ca96787bfbfe31
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2018
ms.locfileid: "52711357"
---
# <a name="tutorial-create-a-quick-chart-report-offline-report-builder"></a>教學課程：離線建立快速圖表報表 (報表產生器)

  在本教學課程中，您會使用精靈在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]分頁報表中建立圓形圖。 然後您會加入百分比，然後稍微修改圓形圖。 
  
您可以採用兩種不同的方式進行此教學課程。 這兩種方法結果都一樣，這個示範的圓形圖會像這樣：  
  
 ![報表產生器快速圓形圖](../../reporting-services/report-builder/media/report-builder-quick-pie-chart.png "報表產生器快速圓形圖")  
  
## <a name="prerequisites"></a>Prerequisites  
 不論您使用的是 XML 資料或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢，都需要具備報表產生器的存取權。 您可以在原生模式或 SharePoint 整合模式中從 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 報表伺服器啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，或者從 Microsoft 下載中心下載 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 。 如需詳細資訊，請參閱 [安裝報表產生器](../../reporting-services/install-windows/install-report-builder.md)。  
  
##  <a name="TwoWays"></a> 進行此教學課程的兩種方式  
  
-   [使用 XML 資料建立圓形圖](#CreatePieChartXML)  
  
-   [建立含資料之 Transact-SQL 查詢的圓形圖](#CreatePieQueryData)  
  
### <a name="using-xml-data-for-this-tutorial"></a>在此教學課程中使用 XML 資料  
 您可以使用從本主題複製的 XML 資料，並將它貼入精靈中。 您不需要連接至原生模式或 SharePoint 整合模式中的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器，也不需要存取 SQL Server 的執行個體。  
  
 [使用 XML 資料建立圓形圖](#CreatePieChartXML)  
  
### <a name="using-a-includetsqlincludestsql-mdmd-query-that-contains-data-for-this-tutorial"></a>針對此教學課程使用包含資料的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢  
 您可以從本主題複製包含資料的查詢，並將它貼入精靈中。 您將需要 SQL Server 執行個體的名稱，以及能夠以唯讀方式存取任何資料庫的認證。 教學課程中的資料集查詢會使用常值資料，但是查詢必須經過 SQL Server 執行個體處理，才能傳回報表資料集所需的中繼資料。  
  
 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢的優點在於，所有其他 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 教學課程都使用相同的方法，因此當您進行其他教學課程時，已經知道要執行哪些作業。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢需要其他幾項必要條件。 如需詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../../reporting-services/prerequisites-for-tutorials-report-builder.md)。  
  
 [建立含資料之 Transact-SQL 查詢的圓形圖](#CreatePieQueryData)  
  
##  <a name="CreatePieChartXML"></a> 使用 XML 資料建立圓形圖  
  
1.  從[Web 入口網站，或 SharePoint 整合模式中的報表伺服器，或從您的電腦](../../reporting-services/report-builder/start-report-builder.md) 啟動報表產生器 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。  
  
     此時會出現 **[使用者入門]** 對話方塊。  
  
     ![開始使用報表產生器](../../reporting-services/media/rb-getstarted.png "開始使用報表產生器")  
  
     如果 [使用者入門] 對話方塊沒有出現，請按一下 [檔案] >[新增]。 [新報表或資料集] 對話方塊大部分的內容和 [使用者入門] 對話方塊相同。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中按一下 [圖表精靈]，然後按一下 [建立]。  
  
4.  在 [選擇資料集] 頁面中按一下 [建立資料集]，然後按一下 [下一步]。  
  
5.  在 [選擇與資料來源的連線] 頁面中，按一下 [新增]。  
  
     **[資料來源屬性]** 對話方塊隨即開啟。  
  
6.  您可以將資料來源命名為任何想要的名稱。 在 [名稱] 方塊中，鍵入 **MyPieChart**。  
  
7.  在 [選取連線類型] 方塊中，按一下 [XML]。  
  
8.  按一下 [認證] 索引標籤，並選取 **[使用目前的 Windows 使用者。可能需要 Kerberos 委派]**，然後按一下 [確定]。  
  
9. 在 [選擇與資料來源的連線] 頁面中，按一下 [MyPieChart]，然後按一下 [下一步]。  
  
10. 複製下列文字並貼入 [設計查詢] 頁面頂端的大型方塊中。  
  
    ```  
    <Query>  
    <ElementPath>Root /S  {@Sales (Integer)} /C {@FullName} </ElementPath>  
    <XmlData>  
    <Root>  
    <S Sales="150">  
      <C FullName="Jae Pak" />  
    </S>  
    <S Sales="350">  
      <C FullName="Jillian  Carson" />  
    </S>  
    <S Sales="250">  
      <C FullName="Linda C Mitchell" />  
    </S>  
    <S Sales="500">  
      <C FullName="Michael Blythe" />  
    </S>  
    <S Sales="450">  
      <C FullName="Ranjit Varkey" />  
    </S>  
    </Root>  
    </XmlData>  
    </Query>  
    ```  
  
11. (選擇性) 按一下 [執行] 按鈕 (**!**) 來查看您報表所依據的資料。  
  
     ![報表產生器設計查詢](../../reporting-services/report-builder/media/rb-designquery.png "報表產生器設計查詢")  
  
12. 按 [下一步] 。  
  
13. 在 [選擇圖表類型] 頁面中，按一下 [圓形圖]，然後按一下 [下一步]。  
  
14. 在 [排列圖表欄位] 頁面中，按兩下 [可用的欄位] 方塊中的 **Sales** 欄位。  
  
     請注意，它會自動移至 [值] 方塊，因為它是數值。  
  
     ![報表產生器精靈排列欄位](../../reporting-services/report-builder/media/rb-wizarrangefields.png "報表產生器精靈排列欄位")  
  
15. 將 **FullName** 欄位從 [可用的欄位] 方塊拖曳至 [類別目錄] 方塊中 (或是按兩下該欄位，就會移至 [類別目錄] 方塊)，然後按一下 [下一步]。  
  
     [預覽] 頁面會顯示有代表性資料的新圓形圖。 圖例會顯示成 Full Name 1、Full Name 2，以此類推，而非銷售人員的名稱，而且圓形圖配量的大小也不正確。 這只是要讓您了解報表即將呈現的外觀而已。  
  
     ![報表產生器的新圖表預覽](../../reporting-services/report-builder/media/rb-newchartpreview.png "報表產生器的新圖表預覽")  
  
16. 按一下 **[完成]**。  
  
     現在，您會在 [設計檢視] 中看到新的圓形圖報表，仍有代表性的資料。  
  
     ![報表產生器在設計檢視中的新圓形圖](../../reporting-services/report-builder/media/rb-newpiedesign.png "報表產生器在設計檢視中的新圓形圖")  
  
17. 若要查看實際的圓形圖，請在功能區的 [主資料夾] 索引標籤上，按一下 [執行]。  
  
     ![報表產生器的新圖表執行](../../reporting-services/report-builder/media/rb-newchartrun.png "報表產生器的新圖表執行")  
  
18. 若要繼續修改您的圓形圖，請移至本文中的 [執行精靈之後](#AfterWizard) 。  
  
##  <a name="CreatePieQueryData"></a> 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢建立圓形圖  
  
1.  從[Web 入口網站，從 SharePoint 整合模式中的報表伺服器，或從您的電腦](../../reporting-services/report-builder/start-report-builder.md) 啟動報表產生器 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] web portal, 啟動報表產生器 report server in SharePoint integrated mode, or from your computer.  
  
     此時會出現 **[使用者入門]** 對話方塊。  
  
    > [!NOTE]  
    >  如果 [使用者入門] 對話方塊沒有出現，請按一下 [檔案] >[新增]。 [新報表或資料集] 對話方塊大部分的內容和 [使用者入門] 對話方塊相同。  
  
2.  在左窗格中，確認已選取 **[新增報表]** 。  
  
3.  在右窗格中按一下 [圖表精靈]，然後按一下 [建立]。  
  
4.  在 [選擇資料集] 頁面中按一下 [建立資料集]，然後按一下 [下一步]。  
  
5.  在 [選擇與資料來源的連線] 頁面中，選取現有的資料來源，或瀏覽至報表伺服器並選取資料來源，然後按一下 [下一步]。 您可能需要輸入使用者名稱和密碼。  
  
    > [!NOTE]  
    >  只要您有適當的權限，選擇哪一種資料來源都無關緊要。 因為您不會從資料來源取得資料。 如需詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../../reporting-services/prerequisites-for-tutorials-report-builder.md)。  
  
6.  在 **[設計查詢]** 頁面上，按一下 **[當成文字編輯]**。  
  
7.  將下列查詢貼入查詢窗格中：  
  
    ```  
    SELECT 150 AS Sales, 'Jae Pak' AS FullName   
    UNION SELECT 350 AS Sales, 'Jillian Carson' AS FullName   
    UNION SELECT 250 AS Sales, 'Linda C Mitchell' AS FullName   
    UNION SELECT 500 AS Sales, 'Michael Blythe' AS FullName   
    UNION SELECT 450 AS Sales, 'Ranjit Varkey' AS FullName   
    ```  
  
8.  (選擇性) 按一下 [執行] 按鈕 (**!**) 來查看您圖表所依據的資料。  
  
9. 按 [下一步] 。  
  
10. 在 [選擇圖表類型] 頁面中，按一下 [圓形圖]，然後按一下 [下一步]。  
  
11. 在 [排列圖表欄位] 頁面中，按兩下 [可用的欄位] 方塊中的 **Sales** 欄位。  
  
     請注意，它會自動移至 [值] 方塊，因為它是數值。  
  
12. 將 **FullName** 欄位從 [可用的欄位] 方塊拖曳至 [類別目錄] 方塊中 (或是按兩下該欄位，就會移至 [類別目錄] 方塊)，然後按一下 [下一步]。  
  
13. 按一下 **[完成]**。  
  
     您現在就會在設計介面上看見新的圓形圖報表。 您所看見的內容是代表性內容。 圖例會顯示成 Full Name 1、Full Name 2，以此類推，而非銷售人員的名稱，而且圓形圖配量的大小也不正確。 這只是要讓您了解報表即將呈現的外觀而已。  
  
15. 若要查看實際的圓形圖，請在功能區的 [主資料夾] 索引標籤上，按一下 [執行]。  
 
##  <a name="AfterWizard"></a> 執行精靈之後  
 既然您已經擁有圓形圖報表，就可以開始處理它。 在 [功能區] 的 [執行] 索引標籤上，按一下 [設計]，即可繼續修改。  
  
## <a name="make-the-chart-bigger"></a>讓圖表變大  
 您可能想要讓圓形圖變大。 
 
*  按一下以選取圖表 (而非圖表中的任何元素)，然後拖曳右下角調整其大小。  

請注意，設計介面會隨著您拖曳而變得較大。
  
## <a name="add-a-report-title"></a>加入報表標題  
1. 選取圖表頂端的 [圖表標題] 這幾個字，然後輸入標題，例如**銷售圓形圖**。  
2. 在選取標題的情況下，將 [屬性] 窗格中的 [色彩] 變更為 [黑色]，將 [字型] 變更為 [12 pt]。
  
## <a name="add-percentages"></a>加入百分比  
 
1.  以滑鼠右鍵按一下圓形圖，然後選取 [顯示資料標籤]。 資料標籤會顯示在圓形圖的每個扇形區內。  
  
2.  以滑鼠右鍵按一下標籤，然後選取 [數列標籤屬性]。 [數列標籤屬性] 對話方塊便會出現。  
  
3.  在 [標籤資料] 方塊中，鍵入 **#PERCENT{P0}**。  
  
     **{P0}** 提供您沒有小數位數的百分比。 如果您只鍵入 **#PERCENT**，數字將具有兩個小數位數。 **#PERCENT** 是為您執行計算或函式的關鍵字；還有其他關鍵字可以使用。  
     
4. 按一下 [是] 以確認您要將 **UseValueAsLabel** 設定為 **False**。

5. 在 [字型] 索引標籤上，選取 [粗體]，並將 [色彩] 變更為 [白色]。

6. 按一下 [確定] 。     
  
 如需自訂圖表標籤和圖例的詳細資訊，請參閱 [在圓形圖上顯示百分比值 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md) 和[變更圖例項目的文字 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)。  
  
##  <a name="WhatsNext"></a> 下一步  
 既然您已經在 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]中建立第一份報表，就可以準備嘗試進行其他教學課程，並且根據自己的資料開始建立報表。 若要執行 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]，您需要使用 *連接字串*(實際上會將您連接至資料來源) 來存取資料庫等資料來源的權限。 系統管理員會提供這項資訊而且可能會為您設定。  
  
 若要進行其他教學課程，您需要 SQL Server 執行個體的名稱，以及能夠以唯讀方式存取任何資料庫的認證。 系統管理員可能也會為您進行該設定。  
  
 最後，若要將報表儲存至報表伺服器或與報表伺服器整合的 SharePoint 網站，您將需要 URL 和權限。 雖然您可以直接從電腦執行任何已建立的報表，不過從報表伺服器或 SharePoint 網站執行時，報表會提供更多功能。 您需要權限才能從發行報表的報表伺服器或 SharePoint 網站執行您的報表或其他報表。 請連絡系統管理員以取得存取權。  
  
 開始之前，閱讀一些概念和詞彙的相關資訊可能會有所協助。 請參閱[報表撰寫概念 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)。 此外，在您建立第一份報表之前，請花點時間規劃一下。 這是值得花費的時間。 請參閱[規劃報表 &#40;報表產生器&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md)。  

## <a name="next-steps"></a>後續步驟

[報表產生器教學課程](../../reporting-services/report-builder-tutorials.md)   
[SQL Server 的報表產生器](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
