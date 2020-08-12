---
title: 預先載入快取 (SSRS)| Microsoft Docs
description: 了解如何在 Reporting Services 報表伺服器中透過為共用資料集建立快取重新整理計劃，以針對共用資料集預先載入快取。
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- cache [Reporting Services]
- preloading cache
ms.assetid: 152a1051-8aa5-4c01-bc85-f8be8971b0cd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5401d324be7bb59d5be21afa72acebc0a7ab6487
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84548040"
---
# <a name="preload-the-cache"></a>預先載入快取  
  您可以為共用資料集建立快取重新整理計劃，為共用資料集預先載入快取。  
  
 您有兩種方式，可以預先載入報表的快取：  
  
1.  建立報表的快取重新整理計劃。 這是慣用的方法。  
  
2.  使用資料驅動訂閱，以預先載入有參數化報表執行個體的快取。 這是在早於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)][!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]的版本中預先載入快取的唯一方法。 如需詳細資訊，請參閱 [快取報表 &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)的版本中預先載入快取的唯一方法。  
  
 快取報表或共用資料集之前，必須符合下列條件：  
  
-   共用資料集或報表必須已啟用快取。  
  
-   共用資料集或報表的共用資料來源必須設定為使用預存的認證或無認證。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務必須執行。  
  
## <a name="to-preload-the-cache-by-creating-a-cache-refresh-plan"></a>若要透過建立快取重新整理計劃以預先載入快取  
  
1. 啟動[報表伺服器的入口網站](../../reporting-services/web-portal-ssrs-native-mode.md "報表伺服器的入口網站")。  
  
2. 從主畫面選取 [瀏覽]，並瀏覽資料夾階層以尋您要建立的項目。  
  
3. 選取項目右上角的省略，然後從下拉式功能表選取 [管理]。  
  
4. 選取左邊的垂直功能表中的 [快取] 索引標籤。  
  
5. 若要為資料集啟用快取，請選取 [快取此資料集的複本，並在可取得時使用] 選項按鈕。 [快取逾期] 區段接著會出現在它的下方。 選取下列其中一個選項按鈕：

    - [快取逾期於 x 分鐘後] \(為 x 輸入想要的分鐘數\)。
    - [快取於排程逾期]。  Reporting Services 提供共用排程與報表特定排程，以協助您控制處理程序、一致的內容與報表散發效能。 如需詳細資訊，請參閱 [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md "Create, Modify, and Delete Schedules")。 您有數個選項可建立排程，在此案例中，為了快取逾期：選取下列兩個排程選項的其中一個：  
      - [共用排程] 選項按鈕，然後從 [選取共用排程] 下拉式文字方塊選取排程。 如需詳細資訊，請參閱 [Schedules](../../reporting-services/subscriptions/schedules.md "排程")。  
      - [報表特定排程] 選項按鈕，然後選取 [編輯排程] 連結 (若要顯示 [排程詳細資料] 頁面)。  

         ![資料集的入口網站快取逾期 [排程詳細資料] 頁面](../../reporting-services/report-server/media/preload-the-cache/web-portal-dataset-cache-schedule-details.png "資料集快取排程詳細資料頁面")

          在此頁面上，您可以選取：
         - 排程的類型：
           - **小時** - 執行排程間隔：指定時與分鐘，以及開始時間。
           - **日** - 選取下列三個選擇中的其中一個：  
              - **在下列幾天**：(週日、週一、週二、週三、週四、週五、週六)。
              - **每個工作天**
              - **在此天數後重複** - 指定數字。  
           - **週** - 同時指定下面兩個項目：
              - **在此週數後重複** - 指定數字。  
              - **在幾天** - 挑選星期幾來執行它。  
           - **月** - 哪些月份，選擇有：
              - **在當月的哪一週**，  
                 - 從下拉式清單方塊選取 (第一個、第二個、第三個、第四個或最後一個)。  
                 - **在星期幾**以執行它。 選取一或多個核取方塊 (週日、週一、週二、週三、週四、週五、週六)。  
                 - **行事曆上的日期** -  輸入當月的實際週數 (以逗點分隔)，或輸入一個範圍的日期 (以破折號分隔)，或輸入上述兩者的任意組合 (例如 1,3-5)。  
           - **一次** - 單一發生次數。  
         - **開始時間** - 排程開始的當天時間。  
         - **開始與結束日期** - 指定排程的開始日期並選擇性地指定結束日期。
         - 選取 [套用] 以儲存排程。  
           > [!NOTE]
           > 如果項目並沒有啟用快取，系統會提示您啟用快取。 若要啟用快取，請選取 [確定]。  

         - 選取 [建立快取重新整理計劃] 以建立/儲存快取計劃。  
         [快取重新整理計劃] 頁面隨即在畫面上開啟。 從這裡，您可以：
           - 新增快取重新整理計劃。
           - 從現有計劃建立新的快取重新整理計劃。
           - 重新整理 [快取重新整理計劃] 頁面。
           - 刪除計劃。
           - 依名稱搜尋計劃。

         如果尚未儲存任何快取重新整理計劃，清單將會是空的，而且 [加入] 選擇是唯一可用選項。 選取 [+ 新增快取重新整理計劃] 以新增快取重新整理計劃，[新增快取重新整理計劃] 頁面隨即顯示。  
           - 在第一個文字方塊中輸入 [描述] 以命名該重新整理計劃。  
           - 在 [依下列排程來重新整理快取] 中選取下列其中一個選項按鈕  
             - **共用排程** - 從鄰近的下拉式清單方塊選取共用排程。 
             - **報表特定排程** - 如上面的步驟 2.2 所述編輯排程，方式是選取 [編輯排程]**** 連結 (若要顯示 [排程詳細資料]** 頁面)。 
             - 選取 [建立快取重新整理計劃] 以儲存計劃 (如果是新增計劃)，或選取 [套用] (如果是編輯計劃)。  
      您會返回更新的 [快取重新整理計劃] 頁面。
  
## <a name="to-preload-the-cache-with-a-user-specific-report-by-using-a-data-driven-subscription"></a>若要透過使用資料驅動訂閱以預先載入含使用者專屬報表的快取

1. 啟動[報表伺服器的入口網站](../../reporting-services/web-portal-ssrs-native-mode.md "報表伺服器的入口網站")。  
2. 從主畫面選取 [瀏覽]，並瀏覽資料夾階層以尋您要訂閱的報表。  
3. 以滑鼠右鍵按一下報表，從下拉式功能表選取 [訂閱]。 [新的訂用帳戶] 頁面隨即顯示。  
4. 在 [描述] 文字方塊中，輸入訂用帳戶的描述。  
5. [訂閱類型] 選項按鈕會顯示兩個選項：  
   - **標準訂閱** - 以產生及傳遞一份報表
   - **資料驅動訂閱** - 以為資料集內的每一個資料列，產生及傳遞一份報表。 這是您想要選取以預先載入快取的選項。
6. 在 [排程] 區段中，選取下列其中一個選項按鈕：
   - **共用排程** - 從下拉式清單方塊選取共用排程。  
   - **報表特定排程** - 如上面的步驟 2.2 所述編輯排程，方式是選取 [編輯排程]**** 連結 (若要顯示 [排程詳細資料]** 頁面)。  
7. [目的地] 區段會在下拉式清單方塊中顯示下列選項：
    - **Windows 檔案共用**
    - **電子郵件**
    - **Null 傳遞提供者** - 針對此工作，請選取 Null 傳遞提供者。  
8. 在 [資料集] 區段中，編輯或建立此報告訂閱的資料集，方式是選取 [編輯資料集] 按鈕。  
9. 在 [編輯資料集]**** 頁面的 [資料來源]**** 區段中，選擇包含報告參數值與傳遞選項的資料來源。 您的選擇有：  
   - **共用的資料來源** - 選取省略符號，然後從共用的資料來源選取 [共用資料來源] 資料夾。
   - **自訂資料來源** - 最有可能。 這是您必須選擇的選項，除非您或其他人已完成下列步驟以建立它並作為共用資料來源。  
     - 指定連接類型、連接字串和認證，以存取包含訂閱者資料的資料來源。 下列範例將說明用來連接到名為 Subscribers 之 SQL Server 資料庫的連接字串。  
  
   ```T-SQL
   data source=<servername>;initial catalog=Subscribers  
   ```
  
10. 在 [查詢] 區段中 - 指定擷取所需訂閱者資料的查詢。  例如：  
  
    ```T-SQL  
    Select * from RptSubscribers  
    ```
  
    選擇性地增加花較長時間處理之查詢的逾時期間。  
  
11. 選取 [驗證]。 必須先驗證查詢，才能繼續。 當 [驗證成功] 訊息出現時，[驗證] 按鈕下將顯示資料集欄位清單。 選取 [套用] 以建立自訂資料來源。  
  
12. 您會回到 [新的訂用帳戶]頁面。  在 [報表參數] 區段中，為顯示的報表參數 (如果有的話) 指定報表參數值  

13. 選取 [建立訂閱]。  
  
14. [訂閱] 頁面隨即顯示，其中顯示您的新資料驅動訂閱。 從這個頁面，您可以在準備好時啟用訂閱，方式是選取它左邊的核取方塊，然後選取 [啟用]**** 按鈕。 ![[訂閱] 頁面的 [啟用] 按鈕](../../reporting-services/report-server/media/preload-the-cache/subscriptions-page-enable-button.png "訂閱頁面上的啟用按鈕")

15. 指定處理訂閱的時間。 請勿選擇 [更新報表伺服器上的報表資料時]。 該設定僅適用於快照集。 如果您想要使用預先存在的排程，請選取 [在共用排程上]。  
  
     或者，若要建立自訂排程，請選取 [在為此訂閱建立的排程上] ，然後選取 [下一步]。 設定排程，然後選取 [完成]。  
  
    > [!NOTE]  
    > 為了讓訂閱者能夠接收到最新的報表，您設定的排程應該與您為訂閱者所定義的報表傳遞排程一致。 如需詳細資訊，請參閱[報表伺服器的入口網站](../../reporting-services/web-portal-ssrs-native-mode.md  "報表伺服器的入口網站")。  
  
16. 設定報表的執行選項，如下。 在報表頁面上，選取 [屬性] 索引標籤。  
  
17. 在左框架內，按一下 [執行] 索引標籤。  
  
18. 在頁面上，選取 **[以最新的資料轉譯此報表]** 。  
  
19. 選擇下列兩個快取選項的其中之一並設定逾期，如下：  
  
    - 若要將快取副本設定在特定時段之後過期，請選取 [快取報表的暫存副本。**報表副本會在下列分鐘數後過期]。** 輸入報表過期的分鐘數。  
  
    - 若要使快取複本依據排程過期，請按一下 [快取報表的暫存副本。**在下列排程上使報表的副本過期]。** 選取 [設定]，或選取共用排程來設定報表過期的排程。  
  
20. 選取 [套用]。
  
## <a name="see-also"></a>另請參閱  

 [資料驅動訂閱](../../reporting-services/subscriptions/data-driven-subscriptions.md)  
 [建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
 [效能、快照集、快取 &#40;Reporting Services&#41;](../../reporting-services/report-server/performance-snapshots-caching-reporting-services.md)  
 [設定報表處理屬性](../../reporting-services/report-server/set-report-processing-properties.md)  
 [快取報表 &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
 [使用共用資料集](../../reporting-services/work-with-shared-datasets-web-portal.md)  
  
