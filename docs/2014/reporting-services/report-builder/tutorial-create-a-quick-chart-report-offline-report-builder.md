---
title: 教學課程：離線建立快速圖表報表 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports, creating
- tutorials, getting started
- creating reports
ms.assetid: 6b1db67a-cf75-494c-b70c-09f1e6a8d414
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5cd666ec589737d83717e9b435a260bd2a0d0ef6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176892"
---
# <a name="tutorial-create-a-quick-chart-report-offline-report-builder"></a>教學課程：離線建立快速圖表報表 (報表產生器)
  在此教學課程中，您將使用精靈來建立圓形圖，然後稍微進行修改，以便了解可行的作業。 您可以採用兩種不同的方式進行此教學課程。 這兩種方法的結果都相同，如下圖所示的圓形圖：

 ![[執行] 檢視中的「我的第一個圓形圖」](../media/rs-my1stpierunview.gif "[執行視圖] 中的第一個圓形圖")

## <a name="prerequisites"></a>Prerequisites
 不論您使用的是 XML 資料或 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查詢，都需要具備 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 報表產生器的存取權。 您可以執行單機版，或者報表管理員或 SharePoint 網站提供的 ClickOnce 版本。 只有第一個步驟「如何開啟報表產生器」與 ClickOnce 版本不同。 如需詳細資訊，請參閱[安裝、卸載和報表產生器支援](../install-uninstall-and-report-builder-support.md)。

##  <a name="two-ways-to-do-this-tutorial"></a><a name="TwoWays"></a> 進行此教學課程的兩種方式

-   [使用 XML 資料建立圓形圖](#CreatePieChartXML)

-   [建立含資料之 Transact-SQL 查詢的圓形圖](#CreatePieQueryData)

### <a name="using-xml-data-for-this-tutorial"></a>在此教學課程中使用 XML 資料
 您可以使用從本主題複製的 XML 資料，並將它貼入精靈中。 您不需要連接至報表伺服器或是 SharePoint 整合模式中的報表伺服器，也不需要存取 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 執行個體。

 [使用 XML 資料建立圓形圖](#CreatePieChartXML)

### <a name="using-a-transact-sql-query-that-contains-data-for-this-tutorial"></a>在此教學課程中使用包含資料的 Transact-SQL 查詢
 您可以從本主題複製包含資料的查詢，並將它貼入精靈中。 您將需要 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 執行個體的名稱，以及能夠以唯讀方式存取任何資料庫的認證。 教學課程中的資料集查詢會使用常值資料，但是查詢必須經過 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 執行個體處理，才能傳回報表資料集所需的中繼資料。

 使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查詢的優點在於，所有其他報表產生器教學課程都使用相同的方法，因此當您進行其他教學課程時，已經知道要執行哪些作業。

 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查詢需要其他幾項必要條件。 如需詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../report-builder-tutorials.md)。

 [建立含資料之 Transact-SQL 查詢的圓形圖](#CreatePieQueryData)

## <a name="also-in-this-article"></a>本文相關內容
 [執行嚮導之後](#AfterWizard)

 [下一步](#WhatsNext)

##  <a name="creating-the-pie-chart-with-xml-data"></a><a name="CreatePieChartXML"></a>使用 XML 資料建立圓形圖

#### <a name="to-create-the-pie-chart-with-xml-data"></a>建立含 XML 資料的圓形圖

1.  按一下 **[開始]**、依序指向 **[程式集]** 和 **[Microsoft SQL Server 2012 報表產生器]**，然後按一下 **[報表產生器]**。

     [**消費者入門**] 對話方塊隨即出現。

    > [!NOTE]
    >   如果 **[使用者入門]** 對話方塊沒有出現，請在 **[報表產生器]** 按鈕中按一下 **[新增]**。

2.  在左窗格中，確認已選取 **[報表]** 。

3.  在右窗格中按一下 [圖表精靈]  ，然後按一下 [建立]  。

4.  在 [選擇資料集]  頁面中按一下 [建立資料集]  ，然後按一下 [下一步]  。

5.  在 [選擇與資料來源的連線]  頁面中，按一下 [新增]  。

     **[資料來源屬性]** 對話方塊隨即開啟。

6.  您可以將資料來源命名為任何想要的名稱。 在 [名稱]  方塊中，鍵入 **MyPieChart**。

7.  在 [**選取連線類型**] 方塊中，按一下 [ **XML]。**

8.  按一下 [**認證**] 索引標籤，選取 [**使用目前的 Windows 使用者]。可能需要 Kerberos 委派**，然後按一下 **[確定]**。

9. 在 [選擇與資料來源的連線]  頁面中，按一下 [MyPieChart]  ，然後按一下 [下一步]  。

10. 複製下列文字，並將它貼入 [**設計查詢**] 頁面中央的大型方塊中。

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

12. 按 [下一步]  。

13. 在 [選擇圖表類型]**** 頁面中，按一下 [圓形圖]****，然後按一下 [下一步]****。

14. 在 [排列圖表欄位]**** 頁面中，按兩下 [可用的欄位]**** 方塊中的 **Sales** 欄位。

     請注意，它會自動移至 [值]**** 方塊，因為它是數值。

15. 將 **FullName** 欄位從 [可用的欄位]**** 方塊拖曳至 [類別目錄]**** 方塊中 (或是按兩下該欄位，就會移至 [類別目錄]**** 方塊)，然後按一下 [下一步]****。

16. 在 [**選擇樣式**] 頁面中，預設會選取 [**海洋**]。 按一下其他樣式來查看其外觀。

17. 按一下 [完成]  。

     您現在就會在設計介面上看見新的圓形圖報表。 您所看見的內容是代表性內容。 圖例會顯示成 Full Name 1、Full Name 2，以此類推，而非銷售人員的名稱，而且圓形圖配量的大小也不正確。 這只是要讓您了解報表即將呈現的外觀而已。

18. 若要查看實際的圓形圖，請在功能區的 [主資料夾]**** 索引標籤上，按一下 [執行]****。

 搭配 [![回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首](#TwoWays)

##  <a name="creating-the-pie-chart-with-a-tsql-query"></a><a name="CreatePieQueryData"></a> 使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查詢建立圓形圖

#### <a name="to-create-the-pie-chart-with-a-tsql-query-that-contains-data"></a>若要建立含資料之 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查詢的圓形圖

1.  按一下 **[開始]**、依序指向 **[程式集]** 和 **[Microsoft SQL Server 2012 報表產生器]**，然後按一下 **[報表產生器]**。

2.  在 [**新增報表或資料集**] 對話方塊中，確認已在左窗格中選取 [**報表**]。

3.  在右窗格中按一下 [圖表精靈]****，然後按一下 [建立]****。

4.  在 [選擇資料集]**** 頁面中按一下 [建立資料集]****，然後按一下 [下一步]****。

5.  在 [選擇與資料來源的連線]**** 頁面中，選取現有的資料來源，或瀏覽至報表伺服器並選取資料來源，然後按一下 [下一步]****。 您可能需要輸入使用者名稱和密碼。

    > [!NOTE]
    >  只要您有適當的權限，選擇哪一種資料來源都無關緊要。 因為您不會從資料來源取得資料。 如需詳細資訊，請參閱[教學課程的必要條件 &#40;報表產生器&#41;](../report-builder-tutorials.md)。

6.  在 [**設計查詢**] 頁面上，按一下 [當做**文字編輯**]。

7.  將下列查詢貼入查詢窗格中：

    ```
    SELECT 150 AS Sales, 'Jae Pak' AS FullName 
    UNION SELECT 350 AS Sales, 'Jillian Carson' AS FullName 
    UNION SELECT 250 AS Sales, 'Linda C Mitchell' AS FullName 
    UNION SELECT 500 AS Sales, 'Michael Blythe' AS FullName 
    UNION SELECT 450 AS Sales, 'Ranjit Varkey' AS FullName 
    ```

8.  (選擇性) 按一下 [執行] 按鈕 (**!**) 來查看您報表所依據的資料。

9. 按 [下一步]  。

10. 在 [選擇圖表類型]**** 頁面中，按一下 [圓形圖]****，然後按一下 [下一步]****。

11. 在 [排列圖表欄位]**** 頁面中，按兩下 [可用的欄位]**** 方塊中的 **Sales** 欄位。

     請注意，它會自動移至 [值]**** 方塊，因為它是數值。

12. 將 **FullName** 欄位從 [可用的欄位]**** 方塊拖曳至 [類別目錄]**** 方塊中 (或是按兩下該欄位，就會移至 [類別目錄]**** 方塊)，然後按一下 [下一步]****。

13. 在 [**選擇樣式**] 頁面中，預設會選取 [海洋]。 按一下其他樣式來查看其外觀。

14. 按一下 [完成]  。

     您現在就會在設計介面上看見新的圓形圖報表。 您所看見的內容是代表性內容。 圖例會顯示成 Full Name 1、Full Name 2，以此類推，而非銷售人員的名稱，而且圓形圖配量的大小也不正確。 這只是要讓您了解報表即將呈現的外觀而已。

15. 若要查看實際的圓形圖，請在功能區的 [主資料夾]**** 索引標籤上，按一下 [執行]****。

 搭配 [![回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首](#TwoWays)

##  <a name="after-you-run-the-wizard"></a><a name="AfterWizard"></a> 執行精靈之後
 既然您已經擁有圓形圖報表，就可以開始處理它。 在 [功能區] 的 [執行]**** 索引標籤上，按一下 [設計]****，即可繼續修改。

### <a name="make-the-chart-bigger"></a>讓圖表變大
 您可能想要讓圓形圖變大。 按一下以選取圖表 (而非圖表中的任何元素)，然後拖曳右下角調整其大小。

### <a name="add-a-report-title"></a>加入報表標題
 選取圖表頂端的 [圖表標題]**** 這幾個字，然後輸入標題，例如**銷售圓形圖**。

### <a name="add-percentages"></a>加入百分比

##### <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>將百分比值顯示為圓形圖的標籤

1.  以滑鼠右鍵按一下圓形圖，然後選取 [**顯示資料標籤**]。 資料標籤會顯示在圓形圖的每個扇區內。

2.  以滑鼠右鍵按一下標籤，然後選取 [**數列標籤屬性**]。 [數列標籤屬性]**** 對話方塊便會出現。

3.  針對`#PERCENT{P0}` [**標籤資料**] 選項輸入。

     `{P0}` 提供您沒有小數位數的百分比。 如果您只輸入 `#PERCENT`，數字會有兩個小數位數。 `#PERCENT` 是為您執行計算或函數的關鍵字，還有其他關鍵字可以使用。

 如需自訂圖表標籤和圖例的詳細資訊，請參閱 [在圓形圖上顯示百分比值 &#40;報表產生器及 SSRS&#41;](../report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md) 和[變更圖例項目的文字 &#40;報表產生器及 SSRS&#41;](../report-design/chart-legend-change-item-text-report-builder.md)。

 搭配 [![回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首](#TwoWays)

##  <a name="whats-next"></a><a name="WhatsNext"></a>下一步是什麼？
 既然您已經在報表產生器中建立第一份報表，可以準備嘗試進行其他教學課程，並且根據自己的資料開始建立報表。 若要執行報表產生器，您需要使用*連接字串*來存取資料來源（例如資料庫）的許可權，這會實際將您連接至資料來源。 系統管理員會提供這項資訊而且可能會為您設定。

 若要進行其他教學課程，您需要 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 執行個體的名稱，以及能夠以唯讀方式存取任何資料庫的認證。 系統管理員可能也會為您進行該設定。

 最後，若要將報表儲存至報表伺服器或與報表伺服器整合的 SharePoint 網站，您將需要 URL 和權限。 雖然您可以直接從電腦執行任何已建立的報表，不過從報表伺服器或 SharePoint 網站執行時，報表會提供更多功能。 您需要權限才能從發行報表的報表伺服器或 SharePoint 網站執行您的報表或其他報表。 請連絡系統管理員以取得存取權。

 開始之前，閱讀一些概念和詞彙的相關資訊可能會有所協助。 如需詳細資訊，請參閱[報表產生器和 SSRS&#41;的報表撰寫概念 &#40;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md)。 此外，在您建立第一份報表之前，請花點時間規劃一下。 這是值得花費的時間。 如需詳細資訊，請參閱[規劃報表 &#40;報表產生器&#41;](../report-design/planning-a-report-report-builder.md)。

 搭配 [![回到頁首] 連結使用的箭號圖示](../../2014-toc/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首](#TwoWays)

## <a name="see-also"></a>另請參閱
 [SQL Server 2014 中的](report-builder-in-sql-server-2016.md)[教學課程 &#40;報表產生器&#41;](../report-builder-tutorials.md)報表產生器


