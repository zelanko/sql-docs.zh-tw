---
title: "對 PowerPivot for SharePoint 安裝進行疑難排解 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# 對 PowerPivot for SharePoint 安裝進行疑難排解
  如果您看到的是錯誤，而不是預期的頁面和功能，請執行下列操作。  
  
-   檢閱 SharePoint 和 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的版本資訊，取得已知安裝問題的因應措施。 版本資訊會與安裝媒體一起提供，或是在您下載軟體的 Microsoft 網站上提供。  
  
    -   [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md)  
  
-   請參閱 Technet Wiki 主題：[Troubleshooting Installations of Power Pivot (and other add-ins)](http://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx) (對 Power Pivot 安裝 (及其他增益集) 進行疑難排解)。  
  
## 問題  
  
### PowerPivot 圖庫縮圖顯示為紅色 X  
 其中一個可能的原因是 [網站集合的 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 功能整合] 非使用中。 完成以下動作：  
  
1.  在 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 圖庫文件庫中，從齒輪圖示 ![SharePoint 設定](../analysis-services/media/as-sharepoint2013-settings-gear.png "SharePoint 設定") 或 [首頁] 清單中按一下 [網站設定]。  
  
2.  在 **[網站集合管理]** 區段中，按一下 **[網站集合功能]**。  
  
3.  按一下 **[網站集合功能]**。  
  
4.  確認 [網站集合的 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 功能整合] 為 [使用中]。  
  
 如需此問題的其他原因，請參閱 [Power Pivot Gallery shows Red X's for Icons](http://support.microsoft.com/kb/2361559) (Power Pivot 圖庫的圖示顯示為紅色 X) (http://support.microsoft.com/kb/2361559)。  
  
  