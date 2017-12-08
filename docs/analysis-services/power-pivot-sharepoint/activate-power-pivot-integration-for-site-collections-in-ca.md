---
title: "啟用網站集合，在 CA 中的 Power Pivot 整合 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 62a27e53-446a-42d7-b5db-c009e02d4904
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9958979cc8e0c966ca12c531667d9e05e7dd91f8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="activate-power-pivot-integration-for-site-collections-in-ca"></a>啟用網站集合，在 CA 中的 Power Pivot 整合
  如果您使用 [現有的伺服陣列] 安裝選項來安裝 SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，就需要為特定的網站集合啟用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能整合。 如果您已使用 [新的伺服器] 選項來安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，您可以略過這項工作，因為 SQL Server 安裝程式已經在設定部署時，針對根網站集合啟用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能整合。  
  
 網站集合層級的功能啟用對於將應用程式頁面和範本提供給網站使用 (包括排程資料重新整理的組態頁面，以及 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫和資料摘要文件庫的應用程式頁面) 是必要的。  
  
 您必須為每個支援 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 查詢處理的網站集合啟用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 整合。  
  
## <a name="prerequisites"></a>必要條件  
 您必須是網站集合管理員。  
  
## <a name="activate-power-pivot-features"></a>啟動 Power Pivot 功能  
  
1.  按一下 SharePoint 網站上的 [網站動作]。  
  
     根據預設，SharePoint Web 應用程式會經由通訊埠 80 進行存取。 這表示您通常可以存取 SharePoint 網站輸入 http://\<電腦名稱 > 若要開啟根網站集合。  
  
2.  按一下 **[站台設定]**。  
  
3.  按一下 [網站集合管理] 中的 [網站集合功能]。  
  
4.  向下捲動頁面，直到您找到 [[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 整合網站集合功能]。  
  
5.  按一下 **[啟用]**。  
  
6.  開啟每個網站並按一下 [網站動作]，為其他網站集合重複執行。  
  
## <a name="see-also"></a>請參閱＜  
 [管理中心的 PowerPivot 伺服器管理和組態](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [初始組態 (Power Pivot for SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)   
 [PowerPivot for SharePoint 2010 安裝](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)  
  
  
