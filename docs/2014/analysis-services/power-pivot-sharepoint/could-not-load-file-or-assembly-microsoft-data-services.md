---
title: 無法載入檔案或組件&#39;Microsoft.AnalysisServices.SharePoint.Integration&#39; |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 6e350b67-5e18-4b90-8fb7-a0109cbb27b7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2b8328c060d7096cb43edcbc31206a8b55e82e7e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62749526"
---
# <a name="could-not-load-file-or-assembly-39microsoftanalysisservicessharepointintegration39"></a>無法載入檔案或組件&#39;Microsoft.AnalysisServices.SharePoint.Integration&#39;
  在擁有 PowerPivot for SharePoint 的 SharePoint 2010 環境中，如果 PowerPivot 的應用程式層級方案並未正確部署，將會發生這個錯誤。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用於|PowerPivot for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Powerpivotwebapp 方案未部署或是未正確部署。|  
|訊息文字|無法載入檔案或組件 'Microsoft.AnalysisServices.SharePoint.Integration'|  
  
## <a name="explanation"></a>說明  
 PowerPivot for SharePoint 使用方案套件將它的功能部署到 SharePoint 伺服器上。 其中一個方案未正確部署。 因此，每當您嘗試開啟 SharePoint 網站上的 PowerPivot 圖庫或其他 PowerPivot 應用程式頁面時，都會出現這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
 部署方案套件。  
  
1.  在管理中心的 [系統設定] 中，按一下 **[管理伺服器陣列方案]**。  
  
2.  按一下 [Powerpivotwebapp]。  
  
3.  按一下 **[部署方案]**。  
  
4.  選擇發生這個錯誤的 Web 應用程式。 如果有一個以上的 Web 應用程式，請針對所有應用程式重新部署此方案。  
  
5.  按一下 [確定] 。  
  
## <a name="see-also"></a>另請參閱  
 [將 PowerPivot 方案部署到 SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
