---
title: 無法載入 'Microsoft.AnalysisServices.SharePoint.Integration' |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4da716ab3797f4f6ea54d94c53f753685972df25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208287"
---
# <a name="could-not-load-microsoftanalysisservicessharepointintegration"></a>無法載入 Microsoft.AnalysisServices.SharePoint.Integration
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在擁有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的 SharePoint 2010 環境中，如果 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 的應用程式層級方案並未正確部署，將會發生這個錯誤。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用對象|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Powerpivotwebapp 方案未部署或是未正確部署。|  
|訊息文字|無法載入檔案或組件 'Microsoft.AnalysisServices.SharePoint.Integration'|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 使用方案套件將它的功能部署到 SharePoint 伺服器上。 其中一個方案未正確部署。 因此，每當您嘗試開啟 SharePoint 網站上的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 圖庫或其他 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 應用程式頁面時，都會出現這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
 部署方案套件。  
  
1.  在管理中心的 [系統設定] 中，按一下 **[管理伺服器陣列方案]** 。  
  
2.  按一下 [Powerpivotwebapp]  。  
  
3.  按一下 **[部署方案]** 。  
  
4.  選擇發生這個錯誤的 Web 應用程式。 如果有一個以上的 Web 應用程式，請針對所有應用程式重新部署此方案。  
  
5.  按一下 [確定]  。  
  
## <a name="see-also"></a>另請參閱  
 [將 Power Pivot 解決方案部署到 SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
