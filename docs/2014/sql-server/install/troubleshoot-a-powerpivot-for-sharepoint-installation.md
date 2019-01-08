---
title: 疑難排解 PowerPivot for SharePoint 安裝 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 471bfe1a93e76630e6699a2ff07fcf5c6bddc913
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368600"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>疑難排解 PowerPivot for SharePoint 安裝
  如果您看到的是錯誤，而不是預期的頁面和功能，請執行下列操作。  
  
-   檢閱 SharePoint 和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的版本資訊，取得已知安裝問題的因應措施。 版本資訊會與安裝媒體一起提供，或是在您下載軟體的 Microsoft 網站上提供。  
  
    -   [SQL Server 2014 版本資訊](https://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx)。  
  
-   請參閱 Technet Wiki 主題＜ [PowerPivot 安裝疑難排解 (及其他增益集)](https://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx)＞。  
  
## <a name="issues"></a>問題  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>PowerPivot 圖庫縮圖顯示為紅色的 X  
 其中一個可能的原因是 **[網站集合的 PowerPivot 功能整合]** 非使用中。 完成以下動作：  
  
1.  在 PowerPivot 圖庫文件庫中，按一下**站台設定**從齒輪圖示![SharePoint 設定](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 設定")或**首頁**清單。  
  
2.  在 **[網站集合管理]** 區段中，按一下 **[網站集合功能]**。  
  
3.  按一下 **[網站集合功能]**。  
  
4.  確認 **[網站集合的 PowerPivot 功能整合]** 為 **[使用中]**。  
  
 此問題的其他原因，請參閱 < [PowerPivot 圖庫顯示為紅色 x 圖示](https://support.microsoft.com/kb/2361559)(https://support.microsoft.com/kb/2361559)。  
  
  
