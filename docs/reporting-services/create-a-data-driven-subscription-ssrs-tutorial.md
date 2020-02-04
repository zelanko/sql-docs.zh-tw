---
title: 建立資料驅動訂用帳戶 (SSRS 教學課程) | Microsoft Docs
ms.date: 05/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: baff01bd8bc02af409a37c5cc1ce193e69663387
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "63194831"
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>建立資料驅動訂閱 (SSRS 教學課程)
本 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 教學課程將告訴您資料驅動訂閱概念，方法是逐步解說建立資料驅動訂閱的簡單範例來產生篩選過的報表輸出，並將其儲存至檔案共用。 
[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 資料驅動訂閱可讓您依據動態訂閱者資料來自訂和自動化報表的散發。 資料驅動訂閱適用於下列狀況：  
  
-   將報表散發給成員資格可能隨著不同的散發而變更的大型收件者集區。 例如，將月報表透過電子郵件傳送給目前的所有客戶。  
  
-   依據預先定義的準則，將報表散發給特定收件者群組。 例如，將銷售績效報表傳送給組織中的所有銷售經理。
+ 自動產生各種格式的報表 (例如 .xlsx 和 .pdf)。  
  
## <a name="what-you-will-learn"></a>學習內容  
本教學課程分成三個課程：  

| 課程 | 註解 |
| ------ | -------- |
| [第 1 課：建立範例訂閱者資料庫](../reporting-services/lesson-1-creating-a-sample-subscriber-database.md) | 在這一課，您將建立包含訂閱者資訊的資料表本機 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫。 用於篩選的訂單號碼和輸出檔案格式資訊。 |
| [第 2 課：設定報表資料來源屬性](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md) | 在這一課，您將設定報表資料來源，讓報表可以依據排程自動執行。 自動處理需要預存認證。 您也會將報表資料集修改為包含訂閱者資料所提供的參數。 這個參數是用來根據訂單號碼篩選報表資料。 |
| [第 3 課：定義資料驅動訂閱](../reporting-services/lesson-3-defining-a-data-driven-subscription.md) | 在這一課，您將建立資料驅動訂閱。 本課程會逐步引導您完成「資料驅動訂閱精靈」的每個頁面。 |

下圖說明教學課程的基本工作流程：

| 步驟    | 描述 |
| --------|------------ |
| (1)     | 訂閱組態會註明來源報表、排程以及訂閱者資料庫的欄位對應。 |
| (2)     | OrderInfo 資料表包含要用於篩選的 4 個訂單號碼 (每個檔案 1 個)。 這個資料表也包含所產生報表的檔案格式。 |
| (3)     | Adventureworks 資料庫中的資訊會進行篩選，並在報表中傳回。 |
| (4)     | 報表建立於 Orderinfo 資料表中所指定的檔案格式。 |



   ![ssrs_tutorial_datadriven_flow](../reporting-services/media/ssrs-tutorial-datadriven-flow.png) 
  
## <a name="requirements"></a>需求  
資料驅動訂閱通常是由報表伺服器管理員來建立和維護。 建立資料驅動訂閱的步驟需要建立查詢、包含訂閱者資料之資料來源的知識，以及具備較高的報表伺服器權限。  
  
本教學課程使用 *建立基本資料表報表 &#40;SSRS 教學課程&#41;* 教學課程中所建立的 [建立基本資料表報表 &amp;#40;SSRS 教學課程&amp;#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) 報表，以及範例資料庫 **AdventureWorks2014**中的資料。  
  
您的電腦必須安裝下列項目，才能使用此教學課程：  
  
-   支援資料驅動訂閱的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 如需詳細資訊，請參閱 [SQL Server 2017 的版本及功能](../sql-server/editions-and-components-of-sql-server-2017.md)。  
  
-   報表伺服器必須以原生模式執行。 此教學課程中描述的使用者介面是以原生模式報表伺服器為基礎。 雖然 SharePoint 模式報表伺服器也支援訂閱，不過其使用者介面與此教學課程所描述的使用者介面有所不同。  
  
-   SQL Server Agent 服務必須在執行中。  
  
-   包括參數的報表。 本教學課程採用您使用 `Sales Orders` 建立基本資料表報表 &#40;SSRS 教學課程&#41; [建立基本資料表報表 &amp;#40;SSRS 教學課程&amp;#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)中的資料。  
  
-   **AdventureWorks2014** 範例資料庫，它會將資料提供給範例報表。  
  
-   包括範例報表之「管理所有訂閱」工作的 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 角色指派。 定義資料驅動訂閱需要這項工作。 如果您是電腦的管理員，本機管理員的預設角色指派提供必要權限來建立資料驅動訂閱。 如需詳細資訊，請參閱 [在原生模式報表伺服器上授與權限](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)。  
  
-   您有寫入權的共用資料夾。 共用資料夾必須可透過網路連接存取。  
  
**完成這個教學課程的估計時間：** 30 分鐘。 如果您尚未完成基本報表教學課程，還需額外 30 分鐘。  
  
## <a name="see-also"></a>另請參閱  
[資料驅動訂閱](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[建立基本資料表報表 &#40;SSRS 教學課程&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)
 

