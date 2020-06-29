---
title: 維度處理目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimensionprocessingdest.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d2feaf838706b6862eb480dba7d5a6438ae76247
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437845"
---
# <a name="dimension-processing-destination"></a>維度處理目的地
  「維度處理」目的地會載入及處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 維度。 如需維度的詳細資訊，請參閱[維度 &#40;Analysis Services - 多維度資料&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data)。  
  
 「維度處理」目的地包含下列功能：  
  
-   執行累加式、完整或更新處理的選項。  
  
-   錯誤組態，可以指定在發生指定數目的錯誤之後，維度處理是忽略錯誤還是停止。  
  
-   將輸入資料行對應至維度資料表中的資料行。  
  
 如需處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的詳細資訊，請參閱[處理選項和設定 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services)。  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>設定維度處理目的地  
 「維度處理」目的地會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接管理員，以連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或包含目的地所處理之維度的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。 如需相關資訊，請參閱 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md)。  
  
 此目的地擁有一個輸入。 它不支援錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關 **[維度處理目的地編輯器]** 對話方塊中可設定之屬性的詳細資訊，請按一下下列主題之一：  
  
-   [維度處理目的地編輯器 &#40;連線管理員頁面&#41;](../dimension-processing-destination-editor-connection-manager-page.md)  
  
-   [維度處理目的地編輯器 &#40;對應頁面&#41;](../dimension-processing-destination-editor-mappings-page.md)  
  
-   [維度處理目的地編輯器 &#40;進階頁面&#41;](../dimension-processing-destination-editor-advanced-page.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按一下下列其中一個主題：  
  
-   [Common Properties](../common-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](data-flow.md)   
 [Integration Services 轉換](transformations/integration-services-transformations.md)  
  
  
