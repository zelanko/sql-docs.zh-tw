---
title: "編輯資料警示設計工具中的警示 |Microsoft 文件"
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
helpviewer_keywords:
- editing, data alerts
- updating, data alerts
- editing, alerts
- updating, alerts
ms.assetid: dde3664d-90b5-4b12-969e-39152c86e58a
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: bb81e52b160296f57916695f71209ce161e7f802
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="edit-a-data-alert-in-alert-designer"></a>在警示設計工具中編輯資料警示

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../includes/ssrs-appliesto-sql2016-xpreview.md)][!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

從 [資料警示管理員] 開啟您要編輯的資料警示定義。 只有建立警示定義的使用者才能進行編輯。 如需開啟資料警示管理員的詳細資訊，請參閱 [在資料警示管理員中管理我的資料警示](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md)。

> [!NOTE]
> SQL Server 2016 之後已無法再使用 reporting Services 與 SharePoint 整合。

 下圖說明 [資料警示管理員] 中資料警示的內容功能表。  
  
 ![開啟資料警示設計工具，即可編輯](../reporting-services/media/rs-alertmanageriwopendesigner.gif "開啟的資料警示設計工具，按一下 編輯")  
  
 下列程序包括從 [資料警示管理員] 開啟警示定義，以便在 [資料警示設計工具] 中進行編輯的步驟。  
  
### <a name="to-edit-a-data-alert-definition-in-data-alert-designer"></a>在資料警示設計工具中編輯資料警示定義  
  
1.  在 [資料警示管理員] 中，以滑鼠右鍵按一下您要編輯的資料警示定義，然後按一下 [編輯]。  
  
     警示定義會在 [資料警示設計工具] 中開啟。  
  
2.  請更新規則、排程設定和電子郵件設定。 如需詳細資訊，請參閱 [資料警示設計工具](../reporting-services/data-alert-designer.md) 和 [在資料警示設計工具中建立資料警示](../reporting-services/create-a-data-alert-in-data-alert-designer.md)。  
  
    > [!NOTE]  
    >  您無法選擇不同的資料摘要。 若要使用不同的資料摘要，您必須建立新的資料警示定義。  
  
3.  按一下 **[儲存]**。  
  
    > [!NOTE]  
    >  如果報表已變更，而且從報表產生的資料摘要也已變更，則警示定義可能已無效。 當警示定義參考其規則的資料行已從報表中刪除或變更資料類型，或是報表已刪除或移動時，就會發生這種情形。 您可以開啟無效的警示定義，但是無法重新儲存它，除非依據建立定義的目前版本報表資料摘要成為有效的警示定義。 若要深入了解如何從多個報表產生資料摘要，請參閱[從多個報表產生資料摘要 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)。  

## <a name="see-also"></a>另請參閱

[警示系統管理員的資料警示管理員](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Reporting Services Data Alerts](../reporting-services/reporting-services-data-alerts.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
