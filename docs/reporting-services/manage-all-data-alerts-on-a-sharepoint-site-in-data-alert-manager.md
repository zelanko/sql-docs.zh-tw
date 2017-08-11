---
title: "管理資料警示管理員 中的 SharePoint 網站上的所有資料警示 |Microsoft 文件"
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
- managing, alerts
- managing, data alerts
ms.assetid: 9c70b0f4-2db8-4c2e-acbf-96e2a55ddc48
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: abb122ab9eec2ac66895e0b2bc7d1e2dc8490abf
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager"></a>管理資料警示管理員 中的 SharePoint 網站上的所有資料警示

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../includes/ssrs-appliesto-sql2016-xpreview.md)][!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

SharePoint 警示系統管理員可以檢視任何網站使用者建立之資料警示的清單，以及警示的相關資訊。 警示系統管理員還可以刪除警示。 下圖說明 [資料警示管理員] 中可供警示系統管理員使用的功能。

 ![警示系統管理員的 Sharepoint 警示管理員](../reporting-services/media/rs-alertmanagersite.gif "警示管理員讓 Sharepoint 警示管理員")

> [!NOTE]
> SQL Server 2016 之後已無法再使用 reporting Services 與 SharePoint 整合。

## <a name="view-a-list-of-alerts-created-by-a-site-user"></a>檢視網站使用者建立之警示的清單  
  
1.  移至儲存資料警示定義的 SharePoint 網站。  
  
2.  在首頁上，按一下 [網站動作]。  
  
3.  捲動到清單底部，然後按一下 [網站設定]。  
  
4.  在 [Reporting Services] 底下，按一下 [管理資料警示]。  
  
5.  按一下 [檢視使用者的警示] 清單旁邊的向下箭號，然後選取您要檢視其警示的使用者。  
  
6.  按一下 [檢視報表的警示] 清單旁邊的向下箭號，然後選取要檢視的特定警示，或是按一下 [全部顯示]，列出所選取使用者建立的所有警示。  
  
     資料表會列出名稱、報表名稱、資料警示建立者的名稱、傳送資料警示的次數、上一次修改資料警示定義的時間，以及資料警示的狀態。 如果資料警示無法產生或是傳送，狀態資料行就會包含有關錯誤的資訊並協助您疑難排解問題。  
  
## <a name="delete-an-alert-definition"></a>刪除警示定義  
  
-   以滑鼠右鍵按一下您想要刪除的資料警示，然後按一下 [刪除]。  
  
    > [!NOTE]  
    >  您刪除警示之後，就不會再傳送任何警示訊息。 不過，如果您查詢警示資料庫，可能會發現警示定義仍然存在。 警示服務會依照排程執行清除，而警示定義會在下一次清除時永久刪除。 預設的清除間隔是 20 分鐘。 此清除間隔和其他清除間隔都可以加以設定。 如需詳細資訊，請參閱 [Reporting Services 資料警示](../reporting-services/reporting-services-data-alerts.md)。  

## <a name="see-also"></a>請參閱＜

[警示系統管理員的資料警示管理員](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Reporting Services Data Alerts](../reporting-services/reporting-services-data-alerts.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
