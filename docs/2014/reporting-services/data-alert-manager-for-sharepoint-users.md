---
title: SharePoint 使用者的資料警示管理員 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- managing, alerts
- managing, data alerts
ms.assetid: 7b9281c8-2f8b-48f7-85d8-7a7a596e3c82
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6582712e6597c4371beebcdf258145f1fdfb3053
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177008"
---
# <a name="data-alert-manager-for-sharepoint-users"></a>SharePoint 使用者的資料警示管理員
  
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 為 SharePoint 資訊工作者提供了 [資料警示管理員] 以管理資料警示。 資訊工作者可以檢視自己所建立警示的資訊、刪除警示、開啟警示定義進行編輯，以及視需要執行警示。 他們可以選擇僅檢視單一報表的警示，或是所有報表的警示。 下圖說明 [資料警示管理員] 中可供資訊工作者使用的功能。

 ![SharePoint 使用者的警示管理員功能](media/rs-alertmanageriw.gif "SharePoint 使用者的警示管理員功能")

 啟用 SharePoint 網站進行資料警示時，會建立 MyDataAlerts.aspx 和 SiteDataAlerts.aspx 這兩個 SharePoint 頁面，並且將其加入 SharePoint 網站中。 MyDataAlerts.aspx 是 SharePoint 資訊工作者的 [資料警示管理員]。 資訊工作者可以從已建立警示之報表的右鍵功能表開啟 [資料警示管理員]。

 您也可以使用 URL 直接開啟 [資料警示管理員]。 以下說明 URL 的語法：

 `http://<site name>/_layouts/ReportServer/MyDataAlerts.aspx`

> [!NOTE]
>  系統管理員必須先將權限授與您，您才能使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 警示功能。 如需所需權限的資訊，請參閱 [Reporting Services 資料警示](../ssms/agent/alerts.md)。

##  <a name="ViewingAlerts"></a>查看資料警示資訊
 您可以檢視您在 [資料警示設計工具] 中建立之資料警示的清單。 若要開啟 [資料警示管理員]，請在發行至 SharePoint 文件庫的報表上按一下滑鼠右鍵。 下圖顯示報表右鍵功能表上的 [管理資料警示]**** 選項。

 ![從報表操作功能表開啟警示管理員](media/rs-openalertmanager.gif "從報表操作功能表開啟警示管理員")

 [資料警示管理員] 中包含一個資料表，其中列出警示名稱、報表名稱、您的名稱 (也就是警示定義建立者)、送出的警示訊息數目、上一次執行警示的時間、上一次修改警示定義的時間，以及最新的警示訊息狀態。 如果警示訊息無法產生或是傳送，狀態資料行就會包含有關錯誤的資訊並協助您疑難排解警示。 如需詳細資訊，請參閱 [在資料警示管理員中管理我的資料警示](manage-my-data-alerts-in-data-alert-manager.md)。

 下表顯示 [資料警示管理員] 中資料表的範例資料。 當發生錯誤時，資料表的 [狀態]**** 欄位中會包含錯誤訊息和記錄中項目的識別碼 (GUID)。

|警示名稱|報告名稱|建立者|傳送警示|最後執行|上次修改|狀態|
|----------------|-----------------|----------------|-----------------|--------------|-------------------|------------|
|SalesQTR|SalesByTerritoryAndQTR|Lauren Johnson|4|6/12/2011|6/1/2011|上次警示執行成功，並且已傳送警示。|
|UnitsSold|ProductsSalesByQTR|Lauren Johnson|2|7/1/2011|6/28/2011|上次警示執行成功，但因為資料未變更所以未傳送警示。|
|TopPromotion|PromotionTracking|Lauren Johnson|0||5/23/2011|已建立警示。|


##  <a name="DeleteAlerts"></a>刪除資料警示
 您可從 [資料警示管理員] 中刪除警示定義。 身為資訊工作者，您可以刪除自己建立的警示定義。 您無法刪除其他人建立的警示定義。 如需詳細資訊，請參閱 [在資料警示管理員中管理我的資料警示](manage-my-data-alerts-in-data-alert-manager.md)。

 當您刪除警示定義時，會將它永久刪除。 如果您只想要暫停警示訊息，則應變更警示定義中的循環模式或是開始或停止日期。 如需詳細資訊，請參閱 [在警示設計工具中編輯資料警示](edit-a-data-alert-in-alert-designer.md)。



##  <a name="EditAlerts"></a>編輯資料警示
 身為資訊工作者，您可以從 [資料警示管理員] 中開啟警示定義進行編輯。 您可以編輯自己建立的警示定義，但無法編輯其他人建立的警示定義。 您以滑鼠右鍵按一下警示定義，然後按一下 [編輯]****，[資料警示設計工具] 就會開啟，並且顯示警示定義。 如需詳細資訊，請參閱 [資料警示設計工具](../../2014/reporting-services/data-alert-designer.md) 和 [在警示設計工具中編輯資料警示](edit-a-data-alert-in-alert-designer.md)。



##  <a name="RunAlerts"></a>執行資料警示
 [資料警示管理員] 包含上一次警示服務處理資料警示定義的時間，以及已傳送資料警示訊息的次數等相關資訊。 您可能想要立即執行並傳送警示訊息，而不是等到排程指定的時間。 當您從 [資料警示管理員] 執行警示時，會覆寫警示排程，並且在一到五分鐘內開始處理警示定義，這段時間取決於執行報表所需的時間，以及在您選擇執行警示當時報表伺服器的忙碌程度。 不過，如果您指定僅在結果變更時傳送訊息，但結果並未變更，則不會建立或傳送任何訊息。 如需詳細資訊，請參閱 [在資料警示管理員中管理我的資料警示](manage-my-data-alerts-in-data-alert-manager.md)。

> [!NOTE]
>  您按一下 [執行]**** 選項之後，需要幾秒鐘時間更新 [狀態]**** 資料行的值，才會表示警示正在處理。 如果您多次按一下 [執行]**** 選項，則會多次處理警示。 這樣將會不當耗用報表伺服器的資源，並且可能影響報表伺服器的效能。 若要查看有關警示的更新資訊，請按一下網頁瀏覽器的 [重新整理] 按鈕，查看有關警示的狀態更新以及其他資訊。



##  <a name="HowTo"></a> 相關工作
 本節列出如何管理和編輯警示定義的程序。

-   [在資料警示管理員中管理我的資料警示](manage-my-data-alerts-in-data-alert-manager.md)

-   [在警示設計工具中編輯資料警示](edit-a-data-alert-in-alert-designer.md)



## <a name="see-also"></a>另請參閱
 [資料警示設計](../../2014/reporting-services/data-alert-designer.md)工具[在資料警示設計工具中建立資料](create-a-data-alert-in-data-alert-designer.md)警示[Reporting Services 資料警示](../ssms/agent/alerts.md)


