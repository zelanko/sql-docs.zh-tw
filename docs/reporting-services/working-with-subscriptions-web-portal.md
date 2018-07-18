---
title: 處理訂用帳戶 (Web 入口網站) | Microsoft Docs
ms.custom: ''
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 09e8ece5-0200-41f2-87c1-9fab19e261be
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 74ef317fc9546ec54008ac494571c9c00a16d753
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33034235"
---
# <a name="working-with-subscriptions-web-portal"></a>處理訂閱 (Web 入口網站)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

使用 [訂閱] 頁面即可列出目前報表的所有訂閱。 如果您擁有足夠的權限 (如同「管理所有訂閱」工作所表示)，就可以檢視所有使用者的訂閱。 否則，此頁面只會顯示您擁有的訂閱。  
  
建立新訂閱之前，您必須確認報表資料來源是否使用預存認證。 使用 [資料來源屬性] 頁面即可儲存認證。  
  
> [!NOTE]
> 需要啟動 SQL Server Agent 服務。   
  
![ssRSWebPortal-subscriptions1](../reporting-services/media/ssrswebportal-subscriptions1.png)  
   
選取報表的**省略符號 (...)**，並選取 [管理]，然後選取 [訂用帳戶]，即可到達 [訂用帳戶] 頁面。  
  
從 [訂閱] 頁面中，您可以選取 [+ 新增訂閱] 來建立新的訂閱。 您也可以編輯現有訂閱，或刪除所選取的訂閱。  
  
此頁面也會在 [結果] 資料行上提供訂用帳戶執行的結果狀態。 如果訂閱發生錯誤，請先檢查結果資料行，查看訊息為何。  
  
## <a name="creating-or-editing-a-subscription"></a>建立或編輯訂閱  
使用 [新增訂閱] 或 [編輯訂閱] 頁面，即可在報表中建立新的訂閱或修改現有的訂閱。 這個頁面的此選項隨著您的角色指派而改變。 具有進階權限的使用者可以使用額外的選項。  
  
可自主式執行的報表支援訂閱。 報表至少必須使用預存認證或無認證。 如果報表使用參數，就必須指定預設值。 如果您變更報表執行設定或移除參數屬性的預設值，就可能會造成訂閱停用。 如需詳細資訊，請參閱 [建立和管理原生模式報表伺服器的訂閱]。  
  
### <a name="type-of-subscription"></a>訂閱的類型  
您可以選取 [標準訂用帳戶] 和 [資料驅動訂用帳戶]。  
  
![ssRSWebPortal-subscriptions3](../reporting-services/media/ssrswebportal-subscriptions3.png)  
   
資料驅動訂閱會在每次執行訂閱時查詢訂閱者資料庫中的訂閱資訊。 資料驅動訂閱會使用查詢結果來判斷訂閱者收件者、傳遞設定和報表參數值。 在執行時期，報表伺服器執行查詢來取得訂閱設定所用的值。   
  
若要建立資料驅動訂閱，您必須了解如何撰寫取得訂閱資料的查詢或命令。 您必須同時擁有包含訂閱者資料 (例如，訂閱者名稱和電子郵件地址) 的資料存放區，可供訂閱使用。  
  
此選項可供具有進階權限的使用者使用。 如果您要使用預設的安全性，資料驅動訂閱就不可以用於 [我的報表] 資料夾中的報表。  
  
### <a name="destination"></a>目的地  
選取要用來散發報表的傳遞延伸模組。   
  
傳遞延伸模組是否可用，取決於該模組是否安裝和設定於報表伺服器。 報表伺服器電子郵件是預設傳遞延伸模組，但您必須先設定它才能夠使用。 檔案共用傳遞不需要進行設定，但您必須先定義共用資料夾，才能加以使用。  
  
![ssRSWebPortal-subscriptions2](../reporting-services/media/ssrswebportal-subscriptions2.png)  
  
系統會根據您所選取的傳遞延伸模組顯示下列設定：  
  
-   電子郵件訂閱提供電子郵件使用者很熟悉的欄位 (例如，[收件者]、[主旨] 和 [優先順序] 欄位)。 指定 **[包含報表]** 即可內嵌或附加報表，或是指定 **[包含連結]** 以包含連結到報表的 URL。 指定 **[轉譯格式]** 即可為附加或內嵌的報表選擇呈現格式。  
  
-   檔案共用訂閱提供讓您指定目標位置的欄位。 您可以傳遞任何報表至檔案共用。 不過，支援互動式功能的報表 (包括支援針對資料列和資料行向下鑽研的矩陣報表) 將轉譯成靜態檔案。 您無法在靜態檔案中檢視向下鑽研資料列和資料行。 檔案共用的名稱必須以統一命名慣例 (UNC) 格式指定 (例如，\mycomputer\public\myreportfiles)。 在路徑名稱中不可包含反斜線。 報表檔案會使用以轉譯格式為基礎的檔案格式進行傳遞 (例如，如果您選擇 [Excel]，報表就會以 .xlsx 檔案來傳遞)。  
  
### <a name="data-driven-subscription-dataset"></a>資料驅動訂閱資料集  
針對資料驅動訂閱，您必須定義用於訂閱的資料集。 選取 [編輯資料集] 提供該資訊。  
  
![ssRSWebPortal-subscriptions4](../reporting-services/media/ssrswebportal-subscriptions4.png)  
  
您需要先提供用於查詢的 **資料來源** 。 這可以是共用資料來源，或者您可以提供自訂資料來源。  
  
您需要提供 **查詢** ，以列出執行訂閱所需的不同選項。 此畫面將提供需要傳回的欄位。 這些欄位會根據報表的傳遞方法和參數而不同。  
  
為了獲得最佳結果，請先在 SQL Server Management Studio 中執行此查詢，然後再將它用於資料驅動訂閱中。 接著，您可以檢查結果，以便確認它是否包含所需的資訊。 辨識查詢結果的重點包括：  
  
-   結果集中的資料行會決定您可以針對傳遞選項和報表參數指定的值。 例如，如果您要針對電子郵件傳遞建立資料驅動訂閱，就應該擁有電子郵件地址的資料行。  
  
-   結果集中的資料列會決定產生的報表傳遞數目。 如果您有 10,000 個資料列，報表伺服器就會產生 10,000 個通知和傳遞。  
  
![ssRSWebPortal-subscriptions5](../reporting-services/media/ssrswebportal-subscriptions5.png)  
  
接著，您可以驗證查詢。 您也可以定義 **查詢逾時**。  
  
在您建立查詢之後，即可指派必要欄位的值。 您可以輸入手動資料，或從您所建立的資料集中選取欄位。

[入口網站](../reporting-services/web-portal-ssrs-native-mode.md)  
[使用分頁報表](working-with-paginated-reports-web-portal.md)  
[使用共用資料集](../reporting-services/work-with-shared-datasets-web-portal.md)

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
