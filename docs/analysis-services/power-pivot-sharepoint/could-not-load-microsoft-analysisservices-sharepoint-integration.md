---
title: "無法載入檔案或組件 &#39;Microsoft.AnalysisServices.SharePoint.Integration&#39; | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 6e350b67-5e18-4b90-8fb7-a0109cbb27b7
caps.latest.revision: 7
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 7
---
# 無法載入檔案或組件 &#39;Microsoft.AnalysisServices.SharePoint.Integration&#39;
  在擁有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的 SharePoint 2010 環境中，如果 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 的應用程式層級方案並未正確部署，將會發生這個錯誤。  
  
## 詳細資料  
  
|||  
|-|-|  
|適用對象|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Powerpivotwebapp 方案未部署或是未正確部署。|  
|訊息文字|無法載入檔案或組件 'Microsoft.AnalysisServices.SharePoint.Integration'|  
  
## 說明  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 使用方案套件將它的功能部署到 SharePoint 伺服器上。 其中一個方案未正確部署。 因此，每當您嘗試開啟 SharePoint 網站上的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫或其他 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 應用程式頁面時，都會出現這個錯誤。  
  
## 使用者動作  
 部署方案套件。  
  
1.  在管理中心的 [系統設定] 中，按一下 **[管理伺服器陣列方案]**。  
  
2.  按一下 [Powerpivotwebapp]。  
  
3.  按一下 **[部署方案]**。  
  
4.  選擇發生這個錯誤的 Web 應用程式。 如果有一個以上的 Web 應用程式，請針對所有應用程式重新部署此方案。  
  
5.  按一下 **[確定]**。  
  
## 請參閱＜  
 [將 Power Pivot 方案部署到 SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  