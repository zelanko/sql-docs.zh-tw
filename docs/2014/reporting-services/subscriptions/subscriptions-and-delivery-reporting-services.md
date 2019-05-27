---
title: 訂閱與傳遞 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- reports [Reporting Services], distributing
- distributing reports [Reporting Services]
- published reports [Reporting Services], distributing
- sending reports
- sharing reports
- delivering reports [Reporting Services]
- distributing reports [Reporting Services], subscriptions
- subscriptions [Reporting Services], about subscriptions
- subscriptions [Reporting Services]
ms.assetid: be7ec052-28e2-4558-bc09-8479e5082926
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f598946ec6231d1ca5edacf1810431beb4638f88
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66100664"
---
# <a name="subscriptions-and-delivery-reporting-services"></a>Subscriptions and Delivery (Reporting Services)
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 訂閱是在特定時間，或是為了回應某個事件時，以您指定的檔案格式所傳遞之報表組態。 例如，在每個星期三將 MonthlySales.rdl 報表以 Microsoft Word 文件儲存至檔案共用。 訂閱可用於排程及自動化報表的傳遞，並可搭配一組特定的報表參數值。  
  
 您可以為單一報表建立多個訂閱，以區別訂閱選項；例如，您可以指定不同的參數值，以產生三種版本的報表，例如西區銷售額報表、東區銷售額報表及所有銷售額報表。  
  
 ![SSRS 訂閱流程範例](../media/ssrs-subscription-example-flow.png "SSRS 訂閱流程範例")  
  
 並非所有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]版本都提供訂閱。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
> [!NOTE]
>  從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 開始，您可以用程式設計的方式傳送訂閱的擁有權。 沒有任何使用者介面可以用來傳送訂閱的擁有權。 如需詳細資訊，請參閱 <<c0> <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A> 並[使用 PowerShell 變更及清單 Reporting Services Subscription Owners and Run a Subscription](manage-subscription-owners-and-run-subscription-powershell.md)。  
  
 **本主題內容：**  
  
-   [訂閱與傳遞案例](#bkmk_subscription_scenarios)  
  
-   [標準與資料驅動訂閱](#bkmk_standard_and_datadriven)  
  
-   [訂用帳戶需求](#bkmk_subscription_requirements)  
  
-   [傳遞延伸模組](#bkmk_delivery_extensions)  
  
-   [訂用帳戶的組件](#bkmk_parts_of_subscription)  
  
-   [處理訂閱的方式](#bkmk_subscription_processing)  
  
-   [處理訂閱的方式](#bkmk_subscription_processing)  
  
 **本節主題：**  
  
-   [Reporting Services 中的電子郵件傳遞](e-mail-delivery-in-reporting-services.md) ：描述報表伺服器電子郵件傳遞作業和組態。  
  
-   [File Share Delivery in Reporting Services](file-share-delivery-in-reporting-services.md) ：描述報表伺服器檔案共用傳遞作業和組態。  
  
-   [SharePoint Library Delivery in Reporting Services](sharepoint-library-delivery-in-reporting-services.md) ：描述 SharePoint 程式庫的訂閱傳遞。  
  
-   [資料驅動訂閱](data-driven-subscriptions.md) ：提供有關使用資料驅動訂閱以自訂執行階段報表輸出的資訊。  
  
-   [建立及管理原生模式報表伺服器的訂閱](../create-manage-subscriptions-native-mode-report-servers.md)  
  
-   [建立及管理 SharePoint 模式報表伺服器的訂閱](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
-   [監視 Reporting Services 訂閱](monitor-reporting-services-subscriptions.md)  
  
-   [使用 PowerShell 變更及列出 Reporting Services 訂閱擁有者並執行訂閱](manage-subscription-owners-and-run-subscription-powershell.md)  
  
##  <a name="bkmk_subscription_scenarios"></a> 訂閱與傳遞案例  
 當您為每個訂閱設定傳遞選項時，可用的選項將取決於您選擇的傳遞延伸模組而定。 傳遞延伸模組是支援某些散發方式的模組。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包含數種傳遞延伸模組，且可透過協力廠商取得傳遞延伸模組。  
  
 如果您是開發人員，可以建立自訂傳遞延伸模組來支援其他案例。 如需詳細資訊，請參閱 [Implementing a Delivery Extension](../extensions/delivery-extension/implementing-a-delivery-extension.md)。  
  
 下表說明常見的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 訂閱案例。  
  
|狀況|描述|  
|--------------|-----------------|  
|電子郵件報表|給個別使用者和群組的電子郵件報表。 建立訂閱並指定群組別名或電子郵件別名，以接收您要散發的報表。 你可以讓 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 在執行階段決定訂閱資料。 如果您要將相同的報表傳送至成員清單不斷變更的群組，可以使用查詢在執行階段衍生訂閱清單。|  
|離線檢視報表|您要封存的報表可以直接傳送至每晚排程備份的共用資料夾。 在瀏覽器中需要花較長時間載入的大型報表可以採用能夠在桌面應用程式中檢視的格式傳送至共用資料夾。 使用者可為訂閱輸出選取下列其中一種格式：<br /><br /> 包含報表資料的 XML 檔<br /><br /> CSV (逗號分隔)<br /><br /> PDF<br /><br /> MHTML (網頁封存)<br /><br /> Microsoft Excel<br /><br /> TIFF 檔案<br /><br /> Microsoft Word|  
|預先載入快取|如果您有多個參數化報表的執行個體或是大量檢視報表的報表使用者，可以將報表預先載入快取中，以縮短顯示報表所需的處理時間。|  
|資料驅動報表|使用資料驅動訂閱可以在執行階段自訂報表輸出、傳遞選項和報表參數設定。 訂閱會在執行階段使用查詢從資料來源取得輸入值。 您可以使用資料驅動訂閱執行郵件合併作業，將報表傳送至處理訂閱時所決定的訂閱者清單。|  
  
##  <a name="bkmk_standard_and_datadriven"></a> 標準與資料驅動訂閱  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 支援兩種訂閱： **標準** 與 **資料驅動**。 標準訂閱是由個別使用者建立及管理的。 標準訂閱由在訂閱處理期間無法改變的靜態值所組成。 針對每一個標準訂閱，都有一個報表呈現方式選項、傳遞選項和報表參數的集合。  
  
 資料驅動訂閱會透過查詢提供用於指定收件者、報表參數或應用程式格式之值的外部資料來源，在執行階段取得訂閱資訊。 如果您的收件者清單很大，或者想要變化每個收件者的報表輸出，就可以使用資料驅動訂閱。 若要使用資料驅動訂閱，您必須具備建立查詢和了解參數使用方式的專門技術。 報表伺服器管理員通常會建立和管理這些訂閱。 如需詳細資訊，請參閱下列內容：  
  
-   [資料驅動訂閱](data-driven-subscriptions.md)  
  
-   [建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)  
  
##  <a name="bkmk_subscription_requirements"></a> 訂用帳戶需求  
 在建立對報表的訂閱之前，必須符合下列必要條件：  
  
|需求|描述|  
|-----------------|-----------------|  
|Permissions|您必須擁有報表存取權。 在訂閱報表之前，必須擁有檢視報表的權限。<br /><br /> 您的角色指派必須包括「管理個別訂閱」工作。|  
|預存認證|若要建立訂閱，報表必須使用預存認證或不使用認證，才能在執行階段擷取資料。 您無法訂閱設定為使用目前使用者之模擬或委派認證來連接至外部資料來源的報表。 預存認證可以是 Windows 帳戶或資料庫使用者帳戶。 如需詳細資訊，請參閱 [指定報表資料來源的認證及連接資訊](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)<br /><br /> 您必須擁有檢視報表和建立個別訂閱的權限。 報表伺服器必須啟用 **[排程的事件和報表傳遞]** 。 如需詳細資訊，請參閱 [建立和管理原生模式報表伺服器的訂閱](../create-manage-subscriptions-native-mode-report-servers.md)。|  
|報表中的使用者相依值|只有在標準訂閱中才可以建立報表的訂閱，將使用者帳戶資訊併入到篩選中，或是當做出現在報表中的文字來併入。 在報表中，使用者帳戶名稱是透過解析為目前使用者的 `User!UserID` 運算式來指定。 在您建立訂閱時，會將建立訂閱的使用者視為目前的使用者。|  
|沒有模型項目安全性|如果「報表產生器」報表是使用模型當做資料來源，而該模型包含模型項目安全性設定，您便無法訂閱此報表。 這項限制中只包含使用模型項目安全性的報表。|  
|參數值|如果報表使用參數，則參數值必須在報表本身、或您所定義的訂閱中指定。 如果在報表中定義了預設值，您就可以設定參數值以使用預設值。|  
  
##  <a name="bkmk_delivery_extensions"></a> 傳遞延伸模組  
 訂閱會在報表伺服器上處理，而且會透過伺服器上所部署的傳遞延伸模組散發。 根據預設，您可以建立將報表傳送至共用資料夾或電子郵件地址的訂閱。 如果報表伺服器是針對 SharePoint 整合模式所設定，您也可以將報表傳送至 SharePoint 文件庫。  
  
 使用者建立訂閱時，可以選擇其中一個可用的傳遞延伸模組，以決定如何傳遞報表。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包含下列傳遞延伸模組。  
  
|傳遞延伸模組|描述|  
|------------------------|-----------------|  
|Windows 檔案共用|將報表當做靜態應用程式檔案傳遞至可在網路上存取的共用資料夾。|  
|電子郵件|將通知或報表當做電子郵件附件或 URL 連結傳遞。|  
|SharePoint 文件庫|將報表當做靜態應用程式檔案傳遞至可從 SharePoint 網站存取的 SharePoint 文件庫。 此網站必須與以 SharePoint 整合模式執行的報表伺服器整合。|  
|[Null]|Null 傳遞提供者是非常特殊的傳遞延伸模組，可用來將準備好檢視的參數化報表預先載入快取中。這個方法不適用於個別訂閱中的使用者。 資料驅動訂閱中的管理員會使用 Null 傳遞來預先載入快取，以便改善報表伺服器的效能。|  
  
> [!NOTE]  
>  報表傳遞是 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 架構的可延伸部分。 協力廠商可以建立自訂傳遞延伸模組，將報表傳送到其他位置或裝置。 如需有關自訂傳遞延伸模組的詳細資訊，請參閱＜ [Implementing a Delivery Extension](../extensions/delivery-extension/implementing-a-delivery-extension.md)＞。  
  
##  <a name="bkmk_parts_of_subscription"></a> 訂用帳戶的組件  
 訂閱定義包含下列組件：  
  
-   可自動執行之報表 (亦即，使用預存認證或不使用認證的報表) 的指標。  
  
-   傳遞方法 (例如，電子郵件) 和傳遞模式的設定 (例如，電子郵件地址)。  
  
-   以特定格式表示報表的轉譯延伸模組。  
  
-   處理訂閱的條件，以事件呈現。  
  
     通常，執行報表的條件是以時間為基礎。 例如，您可能會想要在每個星期二的下午 3:00 (UTC) 執行特定報表 。 不過，如果報表是當做快照集執行，您就可以指定訂閱會在每次重新整理快照集時執行。  
  
-   執行報表時所使用的參數。  
  
     參數是選擇性的，且只有接受參數值的報表可指定。 因為訂閱通常為使用者所擁有，每個訂閱所指定的參數值會有所不同。 例如，不同部門的業務經理會使用傳回其部門資料的參數。 所有參數必須有一個明確定義的值，或有效的預設值。  
  
 訂閱資訊和個別報表一同儲存在報表伺服器資料庫中。 您無法將訂閱與其相關聯的報表分開管理。 請注意，無法將訂閱擴充以包括描述、其他自訂文字或其他元素。 訂閱僅能包含前述項目。  
  
##  <a name="bkmk_subscription_processing"></a> 處理訂閱的方式  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包含排程與傳遞處理器，其可提供排程報表並將報表傳遞給使用者的功能。 報表伺服器會持續回應其監視的事件。 當符合訂閱所定義之條件的事件發生時，報表伺服器將讀取訂閱，以決定如何處理與傳遞報表。 報表伺服器要求在訂閱中指定的傳遞延伸模組。 傳遞延伸模組執行之後，報表伺服器會從訂閱擷取傳遞資訊，並將其傳送至傳遞延伸模組以供處理。  
  
 傳遞延伸模組會以訂閱中所定義的格式轉譯報表，然後傳遞報表或通知到指定的目的地。 如果無法傳遞報表，就會在報表伺服器記錄檔中記錄一個項目。 如果想要支援重試作業，可以設定報表伺服器在第一次嘗試失敗時，重新嘗試傳遞。  
  
### <a name="processing-a-standard-subscription"></a>處理標準訂閱  
 標準訂閱會產生報表的一個執行個體。 報表會傳遞至單一共用資料夾，或訂閱中所指定的電子郵件地址。 報表配置與資料不會改變。 如果報表使用參數，標準訂閱會以報表中每個參數的單一值處理。  
  
### <a name="processing-a-data-driven-subscription"></a>處理資料驅動訂閱  
 資料驅動訂閱可產生多個報表執行個體，傳遞至多個目的地。 報表配置不會變化，但是如果是從訂閱者結果集傳入參數值，報表中的資料可能會有變化。 從資料列集傳入值的時候，各訂閱者端對於報表轉譯方式及報表是附加或連結至電子郵件的傳遞選項，也可能會有所不同。  
  
 資料驅動訂閱可產生大量的傳遞。 報表伺服器會針對資料列集裡的每個資料列建立一個傳遞，資料列集是從訂閱查詢傳回的。  
  
### <a name="report-delivery-characteristics"></a>報表傳遞特性  
 透過標準訂閱傳遞的報表，通常會轉譯成靜態報表。 這些報表不是以最新的報表執行快照集為基礎，就是為了完成傳遞而產生的靜態報表。 如果您在視需要執行之報表的訂閱中選擇 **[包含連結]** 選項，則在您按一下超連結後，報表伺服器會執行報表。  
  
> [!NOTE]  
>  透過 URL 傳遞的報表仍會保持連接到報表伺服器，且可以在檢視之間更新或刪除。 您對訂閱所選擇的傳遞選項決定報表以 URL、內嵌在電子郵件訊息的主體中，或當作附加檔案傳送的方式傳遞。  
  
 透過資料驅動訂閱傳遞的報表，可以在處理訂閱時重新產生。 報表伺服器並不會在報表特定執行個體或其資料集內鎖定，以完成資料驅動訂閱。 如果訂閱對不同訂閱者使用不同參數值，報表伺服器就會重新產生報表，以產生所需的結果。 在報表副本第一次建立與傳遞之後，如果基礎資料更新，在處理時稍後取得報表的使用者，可能就會看到以不同結果集為基礎的資料。 您可以使用以快照集執行的報表，以確保傳遞給所有訂閱者的是相同的報表執行個體。 然而，如果報表正在處理時，發生了快照集的排程更新，則使用者可能仍然會在報表中取得不同資料。  
  
### <a name="triggering-subscription-processing"></a>觸發訂閱處理  
 報表伺服器使用兩種事件來觸發訂閱處理：在排程中指定的時間驅動事件，或快照集更新事件。  
  
 時間驅動觸發程序使用報表特定排程或共用排程，來指定訂閱執行的時機。 若是視需要與快取報表，排程是唯一的觸發程序選項。  
  
 快照集更新事件使用報表快照集的排程更新來觸發訂閱。 您可以依據在報表上設定的報表執行屬性，定義只要以新資料更新了報表，就會觸發的訂閱。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)   
 [[排程]](schedules.md)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [建立及管理原生模式報表伺服器的訂閱](../create-manage-subscriptions-native-mode-report-servers.md)   
 [監視 Reporting Services 訂閱](monitor-reporting-services-subscriptions.md)  
  
  
