---
title: "在 資料警示設計工具中建立資料警示 |Microsoft 文件"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8464ab9d-afe1-4490-955f-9f3319bcbf8d
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5203aab062888ca40ee83ee3f00521d6661defba
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="create-a-data-alert-in-data-alert-designer"></a>在資料警示設計工具中建立資料警示

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../includes/ssrs-appliesto-sql2016-xpreview.md)][!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

您可在 [資料警示設計工具] 中建立資料警示定義。 儲存警示定義之後，可以在 [資料警示設計工具] 中再次開啟、編輯，然後再次儲存警示定義。 如需編輯警示定義的相關資訊，請參閱 [在資料警示管理員中管理我的資料警示](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md) 和 [在警示設計工具中編輯資料警示](../reporting-services/edit-a-data-alert-in-alert-designer.md)。

> [!NOTE]
> SQL Server 2016 之後已無法再使用 reporting Services 與 SharePoint 整合。

## <a name="create-a-data-alert-definition"></a>建立資料警示定義
 
1.  尋找包含要為其建立資料警示定義之報表的 SharePoint 文件庫。  
  
2.  按一下報表。  
  
     報表就會執行。 如果報表參數化，請確認報表顯示的是您要接收其警示訊息的資料。 如果沒有看見您需要的資料行或值，則可能需要使用不同的參數值重新執行報表。  
  
    > [!NOTE]  
    >  您選擇執行報表的參數值會儲存在警示定義中，並且在處理警示定義的過程中重新執行報表時使用。 若要使用不同的參數值，您必須建立新的警示定義。  
  
3.  在 [動作] 功能表上，按一下 [新增資料警示]。  
  
     下圖顯示 [動作] 功能表。  
  
     ![從 SharePoint 文件庫開啟警示設計工具](../reporting-services/media/rs-openalertdesigneriw.gif "從 SharePoint 文件庫開啟警示設計工具")  
  
     [資料警示設計工具] 隨即開啟，並且在資料表中顯示報表所產生之第一個資料摘要的前 100 個資料列。  
  
    > [!NOTE]  
    >  如果您未看見 [新資料警示] 選項，表示 SharePoint 網站上未設定警示服務，或是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本未包含資料警示。 如需詳細資訊，請參閱 [Reporting Services SharePoint 服務和服務應用程式](../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)。  
    >   
    >  如果 [新資料警示] 選項呈現灰色，表示報表資料來源設定為使用整合式安全性認證或提示輸入認證。 若要使用 [新資料警示] 選項，則必須將資料來源更新為使用預存程序或不使用認證。  
  
     資料摘要的名稱會出現在 [報表資料名稱] 下拉式清單。  
  
4.  您也可以選擇性地從 [報表資料名稱] 下拉式清單中選取不同的資料摘要。  
  
     如果未從報表產生任何資料摘要，則無法為該報表建立警示定義。 報表的配置決定每一個資料摘要的內容。 如需詳細資訊，請參閱[從多個報表產生資料摘要 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)。  
  
5.  (選擇性) 在 [警示名稱] 文字方塊中，將預設名稱更新為更有意義的名稱。  
  
     警示定義的預設名稱就是報表名稱。 警示定義名稱不一定要是唯一的，不過這樣可能造成您之後在 [資料警示管理員] 中檢視警示清單時，難以區分各個警示的情況。 建議您使用有意義且唯一的警示定義名稱。  
  
6.  (選擇性) 將預設資料選項從 [資料摘要中的任何資料都有] 變更為 [資料摘要中的任何資料都沒有]。  
  
7.  按一下 [加入規則]。  
  
     資料摘要中的資料行清單隨即出現。  
  
8.  在清單中，選取要在規則中使用的資料行，然後選取比較運算子並輸入臨界值。  
  
     根據所選取資料行的資料類型而定，會列出不同的比較運算子。 如果資料行的資料類型為日期，則規則的臨界值旁邊會顯示一個行事曆圖示。 您可以藉由按一下行事曆中的日期或輸入日期的方式來輸入資料。  
  
     資料警示設計工具提供兩種比較模式：[值輸入模式] 和 [欄位選取模式]。 預設模式為 [值輸入模式]。 只有在處於 [值輸入模式] 模式且使用 [is] 比較時，才可以加入 OR 子句。  
  
9. 若要加入 OR 子句，請按一下向下箭頭，然後按一下 [值輸入模式]。  
  
10. 輸入比較值。  
  
11. (選擇性) 再按一次省略符號 **(…)** 。  
  
     省略符號 **(…)** 會出現在包含第一個子句的那一行。  
  
     OR 子句將加入 AND 規則底下，且包含在規則內。  
  
12. (選擇性) 按一下向下箭頭，選取 [欄位選取模式]，然後選取清單中的資料行。  
  
     您將會發現，您按一下以加入 OR 子句的省略符號 **(…)** 已消失。  
  
13. (選擇性) 再按一次 [加入規則] 即可將其他規則。  
  
     規則是使用 AND 邏輯運算子結合。  
  
14. 在循環清單中選取一個選項。 根據循環的類型輸入間隔。  
  
15. (選擇性) 按一下 [進階]。  
  
16. (選擇性) 輸入不同的日期，或開啟行事曆，然後按一下行事曆中的日期，藉此變更警示訊息開始的日期。  
  
     預設的開始日期為目前日期。  
  
17. (選擇性) 選取位於 [警示停止時間] 旁邊的核取方塊，然後選擇要停止警示訊息的日期。  
  
     根據預設，警示訊息沒有停止日期。  
  
    > [!NOTE]  
    >  停止警示訊息並不會刪除警示定義。 停止警示訊息之後，可以藉由更新開始和停止日期將它重新啟動。 如需刪除警示定義的相關資訊，請參閱[在資料警示管理員中管理我的資料警示](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md)。  
  
18. (選擇性) 清除 [僅在結果變更時傳送訊息] 核取方塊。  
  
     如果您經常傳送警示訊息，重複的資訊可能會造成困擾，因此您不應清除此核取方塊。  
  
19. 輸入警示訊息收件者的電子郵件地址。 以分號分隔地址。  
  
     如果警示定義建立者的電子郵件地址可用，就會加入 [收件者] 方塊中。  
  
20. (選擇性) 在 [主旨] 文字方塊中更新警示訊息的 [主旨]。  
  
     預設的主體為**資料警示的\<資料警示名稱 >**。  
  
21. (選擇性) 在 [描述] 文字方塊中輸入警示訊息的描述。  
  
22. 按一下 **[儲存]**。  

## <a name="see-also"></a>請參閱＜

[資料警示設計工具](../reporting-services/data-alert-designer.md)   
[警示系統管理員的資料警示管理員](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Reporting Services Data Alerts](../reporting-services/reporting-services-data-alerts.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
