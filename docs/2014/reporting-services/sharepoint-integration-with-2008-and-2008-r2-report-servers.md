---
title: SharePoint 整合與 2008年及 2008 R2 報表伺服器 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d9f51c37-b071-45d0-baec-f82fa6db366f
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 807978ec516f065f8bb2e219c33863e89c7fa2c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035152"
---
# <a name="sharepoint-integration-with-2008-and-2008-r2--report-servers"></a>與 2008 及 2008 R2 報表伺服器的 SharePoint 整合
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 版本引進了一種架構，其中 SharePoint 模式現在是以 SharePoint 共用服務為基礎。 在 SharePoint 管理中心內完成的新功能的管理上**管理服務**和**管理員服務應用程式**頁面。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]仍然支援舊版架構為 SharePoint 整合[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]讓您可以將 SharePoint 2010 整合與舊版報表伺服器的 SharePoint 2010 產品的增益集。  
  
 您可在下列位置找到用來管理舊有架構的 SharePoint 管理中心頁面：  
  
1.  從 SharePoint 管理中心按一下**一般應用程式設定**。  
  
2.  群組**SQL Server Reporting Services （2008年和 2008 R2）** 包含的連結和舊有架構的管理頁面  
  
## <a name="server-integration-architecture"></a>伺服器整合架構  
 將報表伺服器與 SharePoint 產品的執行個體整合時，項目和屬性會儲存在 SharePoint 內容資料庫中。 這可以為將會影響內容的儲存、安全性和存取方式的伺服器技術之間，提供更深層級的整合。  
  
 將報表項目和屬性儲存在 SharePoint 內容資料庫中，可以讓您進行下列作業：瀏覽 SharePoint 程式庫以取得報表伺服器內容類型、使用與 SharePoint 網站上所主控之其他商務文件存取控制相同的權限層級和驗證提供者來保護項目的安全性、使用共同作業和文件管理功能來簽入及簽出報表以進行修改、使用警示以便在項目變更時獲得通知，以及在應用程式內的網頁和網站上內嵌或自訂報表檢視器 Web 組件。 如果您在 SharePoint 站台內有足夠的權限，您也可以從共用資料來源產生報表模型，並使用報表產生器來建立報表。  
  
 報表伺服器會繼續提供所有的資料處理、轉譯和傳遞， 也支援快照和報表記錄所有已排程的報表處理。 當您從 SharePoint 網站開啟報表時，報表伺服器端點會連接到報表伺服器、建立工作階段、準備報表處理作業、擷取資料、將報表合併至報表配置中，然後在報表檢視器 Web 組件中加以顯示。 當報表為開啟狀態時，您可以將其匯出為不同的應用程式格式，或藉由鑽研基礎數字或按選相關的報表，與資料進行互動。 匯出和報表互動作業都是在報表伺服器上執行。  
  
 報表伺服器會與 SharePoint 同步處理作業和資料，並追蹤所處理之檔案的相關資訊。 當您修改任何報表伺服器項目的屬性或設定時，變更會儲存在 SharePoint 資料庫中，然後再複製到可以為報表伺服器提供內部儲存的報表伺服器資料庫。  
  
## <a name="related-content"></a>相關內容  
 [在 SharePoint 中啟用報表伺服器和 Power View 整合功能](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)  
 描述如何啟動與舊版報表伺服器整合所需的報表伺服器功能。  
  
  