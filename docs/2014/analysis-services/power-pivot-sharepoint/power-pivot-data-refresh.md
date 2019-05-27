---
title: PowerPivot 資料重新整理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: ac8358a3-ee71-44c7-8ee6-ac7afe3ebaa4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4ab42604fabaa188a74858038e35a8b90a105df8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071223"
---
# <a name="powerpivot-data-refresh"></a>PowerPivot 資料重新整理
  在建立包含 PowerPivot 資料的活頁簿之後，您可能會想要定期重新整理資料，其方式是重新執行查詢或命令，以取得您原先用來建立活頁簿之來源的更新資訊。 此處理序稱為 `data refresh`，而且您可以在 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 中視需要重新整理資料，或是將其當做已排程的作業，在 SharePoint 伺服器陣列中的應用程式伺服器上，以 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 處理序的方式執行。 如需詳細資訊，請參閱：  
  
-   [SharePoint 2010 中的 PowerPivot 資料重新整理](../powerpivot-data-refresh-with-sharepoint-2010.md)  
  
-   [設定 PowerPivot 無人看管的資料重新整理帳戶&#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)  
  
-   [設定 PowerPivot 資料重新整理的預存的認證&#40;PowerPivot for SharePoint&#41;](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
-   [排程資料重新整理&#40;PowerPivot for SharePoint&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md)  
  
-   [檢視資料重新整理記錄&#40;PowerPivot for SharePoint&#41;](view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
> [!NOTE]
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 SharePoint Server 2013 Excel Services 會使用不同的架構來進行 PowerPivot 資料模型的資料重新整理。 SharePoint 2013 支援的架構會運用 Excel Services 做為主要元件來載入 PowerPivot 資料模型。 先前的資料重新整理架構會使用並仰賴在 SharePoint 模式下執行 PowerPivot 系統服務和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的伺服器來載入資料模型。 如需詳細資訊，請參閱下列內容：  
> 
>  -   [SharePoint 2013 中的 PowerPivot 資料重新整理](power-pivot-data-refresh-with-sharepoint-2013.md)  
> -   [升級活頁簿和排程的資料重新整理 &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
