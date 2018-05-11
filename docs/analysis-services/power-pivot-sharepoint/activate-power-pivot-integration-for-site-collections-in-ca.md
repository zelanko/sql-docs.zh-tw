---
title: 啟用網站集合，在 CA 中的 Power Pivot 整合 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0322da0c2fb3a35f66e1ea2b7d1ea12d24d158f4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="activate-power-pivot-integration-for-site-collections-in-ca"></a>啟用網站集合，在 CA 中的 Power Pivot 整合
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  如果您使用 [現有的伺服陣列] 安裝選項來安裝 SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，就需要為特定的網站集合啟用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能整合。 如果您已使用 [新的伺服器] 選項來安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，您可以略過這項工作，因為 SQL Server 安裝程式已經在設定部署時，針對根網站集合啟用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能整合。  
  
 網站集合層級的功能啟用對於將應用程式頁面和範本提供給網站使用 (包括排程資料重新整理的組態頁面，以及 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫和資料摘要文件庫的應用程式頁面) 是必要的。  
  
 您必須為每個支援 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 查詢處理的網站集合啟用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 整合。  
  
## <a name="prerequisites"></a>필수 구성 요소  
 您必須是網站集合管理員。  
  
## <a name="activate-power-pivot-features"></a>啟動 Power Pivot 功能  
  
1.  按一下 SharePoint 網站上的 [網站動作]。  
  
     根據預設，SharePoint Web 應用程式會經由通訊埠 80 進行存取。 這表示您通常可以存取 SharePoint 網站輸入 http://\<電腦名稱 > 若要開啟根網站集合。  
  
2.  按一下 **[站台設定]**。  
  
3.  按一下 [網站集合管理] 中的 [網站集合功能]。  
  
4.  向下捲動頁面，直到您找到 [[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 整合網站集合功能]。  
  
5.  按一下 **[啟用]**。  
  
6.  開啟每個網站並按一下 [網站動作]，為其他網站集合重複執行。  
  
## <a name="see-also"></a>另請參閱  
 [管理中心的 PowerPivot 伺服器管理和組態](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [初始組態 (Power Pivot for SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)   
 [PowerPivot for SharePoint 2010 安裝](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)  
  
  
