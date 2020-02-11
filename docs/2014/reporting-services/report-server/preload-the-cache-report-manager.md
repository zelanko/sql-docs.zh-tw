---
title: 預先載入快取 (報表管理員) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- cache [Reporting Services]
- preloading cache
ms.assetid: 152a1051-8aa5-4c01-bc85-f8be8971b0cd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 98ce4f723c0b4c04b166b01d17e8014567253518
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66103592"
---
# <a name="preload-the-cache-report-manager"></a>預先載入快取 (報表管理員)
  您可以為共用資料集建立快取重新整理計劃，為共用資料集預先載入快取。  
  
 您有兩種方式，可以預先載入報表的快取：  
  
1.  建立報表的快取重新整理計劃。 這是慣用的方法。  
  
2.  使用資料驅動訂閱，以預先載入有參數化報表執行個體的快取。 這是在早於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)][!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]的版本中預先載入快取的唯一方法。 如需詳細資訊，請參閱 [快取報表 &#40;SSRS&#41;](caching-reports-ssrs.md)的版本中預先載入快取的唯一方法。  
  
 快取報表或共用資料集之前，必須符合下列條件：  
  
-   共用資料集或報表必須已啟用快取。  
  
-   共用資料集或報表的共用資料來源必須設定為使用預存的認證或無認證。  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務必須執行。  
  
### <a name="to-preload-the-cache-by-creating-a-cache-refresh-plan"></a>若要透過建立快取重新整理計劃以預先載入快取  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
2.  在報表管理員中，導覽到 **[內容]** 頁面，然後導覽到您要快取的項目。  
  
3.  將滑鼠停留在該項目上方，按一下下拉式清單，然後按一下 [管理]****。  
  
4.  按一下 **[快取重新整理選項]** 索引標籤。  
  
5.  按一下工具列上的 **[新增快取重新整理計劃]**。  
  
    > [!NOTE]  
    >  如果項目並沒有啟用快取，系統會提示您啟用快取。 若要啟用快取，請按一下 **[確定]**。  
  
     [快取重新整理計劃] 頁面隨即開啟。  
  
6.  選擇性地輸入重新整理計劃的描述。  
  
7.  針對共用排程，按一下 **[共用排程]**，然後選取要使用的排程名稱。  
  
     針對自訂排程，按一下 [項目特定排程]****，然後按一下 [設定]****。  
  
8.  設定排程  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-preload-the-cache-with-a-user-specific-report-by-using-a-data-driven-subscription"></a>若要透過使用資料驅動訂閱以預先載入含使用者專屬報表的快取  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
2.  在報表管理員中，導覽至 **[內容]** 頁面，然後導覽至您要建立訂閱的報表。  
  
3.  按一下報表，按一下 [訂閱]**** 索引標籤，然後按一下 [新增資料驅動訂閱]****。  
  
4.  選擇性地輸入訂閱的描述。  
  
5.  從 **[指定通知收件者的方式]** 清單中，選取 **[Null 傳遞提供者]**。  
  
6.  指定資料來源類型，然後按 **[下一步]** 以設定資料來源。  
  
7.  指定連接類型、連接字串和認證，以存取包含訂閱者資料的資料來源。 下列範例將說明用來連接到名為 Subscribers 之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的連接字串：  
  
    ```  
    data source=<servername>; initial catalog=Subscribers  
    ```  
  
8.  按 [下一步]  。  
  
9. 指定擷取訂閱者資料的查詢或命令。 選擇性地增加花較長時間處理之查詢的逾時期間。 例如：  
  
    ```  
    Select * from UserInfo  
    ```  
  
10. 按一下 [驗證]****。 必須先驗證查詢，才能繼續。 出現 **[成功驗證查詢]** 訊息時，請按 **[下一步]**。  
  
11. 您無法設定 Null 傳遞提供者之傳遞延伸模組的設定，所以請按 **[下一步]**。  
  
12. 指定訂閱的報表參數值，然後按 **[下一步]**。  
  
13. 指定處理訂閱的時間。 請勿選擇 **[更新報表伺服器上的報表資料時]**。 該設定僅適用於快照集。 如果您想要使用預先存在的排程，請選取 [在共用排程上]****。  
  
     或者，若要建立自訂排程，請按一下 **[在為此訂閱建立的排程上]** ，然後按 **[下一步]**。 設定排程，然後按一下 **[完成]**。  
  
    > [!NOTE]  
    >  為了讓訂閱者能夠接收到最新的報表，您設定的排程應該與您為訂閱者所定義的報表傳遞排程一致。 如需詳細資訊，請參閱[報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
14. 設定報表的執行選項，如下。 在報表頁面上，按一下 **[屬性]** 索引標籤。  
  
15. 在左框架內，按一下 **[執行]** 索引標籤。  
  
16. 在頁面上，選取 **[以最新的資料轉譯此報表]**。  
  
17. 選擇下列兩個快取選項的其中之一並設定逾期，如下：  
  
    -   若要使快取副本在特定時間週期之後過期，請按一下 **[快取報表的暫存副本。報表複本會在下列分鐘數後過期]**。 輸入報表過期的分鐘數。  
  
    -   若要使快取複本依據排程過期，請按一下 **[快取報表的暫存複本。報表複本會在下列排程過期]**。 按一下 **[設定]**，或選取共用排程來設定報表過期的排程。  
  
18. 按一下 [套用]  。  
  
## <a name="see-also"></a>另請參閱  
 [Data-Driven Subscriptions](../subscriptions/data-driven-subscriptions.md)   
 [&#40;SSRS 教學課程建立資料驅動訂閱&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)   
 [效能、快照、快取 &#40;Reporting Services&#41;](performance-snapshots-caching-reporting-services.md)   
 [設定報表處理屬性](set-report-processing-properties.md)   
 [快取報表 &#40;SSRS&#41;](caching-reports-ssrs.md)  
  
  
