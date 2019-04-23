---
title: 建立資料驅動訂用帳戶 (SSRS 教學課程) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a6e1399c97e77a2b7b0bb68a8022effefb1d4814
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59964104"
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>建立資料驅動訂閱 (SSRS 教學課程)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供了資料驅動訂閱，讓您可以依據動態訂閱者資料來自訂報表的散發。 資料驅動訂閱適用於下列狀況：  
  
-   將報表散發給成員資格可能隨著不同的散發而變更的大型收件者集區。 例如，將月報表散發給目前的所有客戶。  
  
-   依據預先定義的準則，將報表散發給特定收件者群組。 例如，將銷售績效報表傳給組織中的前 10 名銷售經理。  
  
## <a name="what-you-will-learn"></a>學習內容  
 本教學課程使用簡單的範例說明概念，告訴您如何使用資料驅動訂閱。  
  
 本教學課程分成三個課程：  
  
 [第 1 課：建立範例訂閱者資料庫](lesson-1-creating-a-sample-subscriber-database.md)  
 在這一課，您將學習如何建立包含訂閱者資訊的本機 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫。  
  
 [第 2 課：修改報表資料來源屬性](lesson-2-modifying-the-report-data-source-properties.md)  
 在這一課，您將學習如何修改報表資料來源屬性，讓報表能夠自動執行。 自動處理需要預存認證。 您也會將報表資料集修改為包含訂閱者資料所提供的參數。  
  
 [第 3 課：定義資料驅動訂閱](lesson-3-defining-a-data-driven-subscription.md)  
 在這一課，您將學習如何定義資料驅動訂閱。 本課程會逐步引導您完成「資料驅動訂閱精靈」的每個頁面。  
  
## <a name="requirements"></a>需求  
 資料驅動訂閱通常是由報表伺服器管理員來建立和維護。 您必須是建立查詢的專家、擁有包含訂閱者資料之資料來源的知識，且具備較高的報表伺服器權限，才能夠建立資料驅動訂閱。  
  
 本教學課程會使用在本教學課程中建立報表[建立基本資料表報表&#40;SSRS 教學課程&#41;](create-a-basic-table-report-ssrs-tutorial.md)以及來自資料 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]  
  
 您的系統必須已經安裝下列項目，才能使用這個教學課程：  
  
-   支援資料驅動訂閱的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 如需詳細資訊，請參閱 <<c0> [ 版本和 SQL Server 2014 元件](../sql-server/editions-and-components-of-sql-server-2016.md)。  
  
-   報表伺服器必須以原生模式執行。 此教學課程中描述的使用者介面是以原生模式報表伺服器為基礎。 雖然 SharePoint 模式報表伺服器也支援訂閱，不過其使用者介面與此教學課程所描述的使用者介面有所不同。  
  
-   SQL Server Agent 服務必須在執行中。  
  
-   包括參數的報表。 本教學課程採用您使用 `Sales Orders` 建立基本資料表報表 &#40;SSRS 教學課程&#41; [建立基本資料表報表 &amp;#40;SSRS 教學課程&amp;#41;](create-a-basic-table-report-ssrs-tutorial.md)中的資料。  
  
-   [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 範例資料庫，它會將資料提供給範例報表。  
  
-   包括範例報表之「管理所有訂閱」工作的角色指派。 定義資料驅動訂閱需要這項工作。 如果您是電腦的管理員，本機管理員的預設角色指派提供必要權限來建立資料驅動訂閱。 如需詳細資訊，請參閱 [在原生模式報表伺服器上授與權限](security/granting-permissions-on-a-native-mode-report-server.md)。  
  
-   您有寫入權的共用資料夾。 共用資料夾必須可透過網路連接存取。  
  
 **完成這個教學課程的估計時間：** 30 分鐘。 如果您尚未完成基本報表教學課程，還需額外 30 分鐘。  
  
## <a name="see-also"></a>另請參閱  
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [建立基本資料表報表 &#40;SSRS 教學課程&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
