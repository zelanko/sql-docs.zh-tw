---
title: 資料分割處理目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partitionprocessingdest.f1
helpviewer_keywords:
- partitions [Analysis Services], processing
- Partition Processing destination [Integration Services]
- destinations [Integration Services], Partition Processing
ms.assetid: 36c592ff-3f78-4a58-b496-31c1c8eee131
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2d36d354aee299efdeefc38d6000c16f1d0fc6b9
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375026"
---
# <a name="partition-processing-destination"></a>資料分割處理目的地
  「資料分割處理」目的地會載入及處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料分割。 如需資料分割的詳細資訊，請參閱[資料分割 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)。  
  
 「資料分割處理」目的地包含下列功能：  
  
-   執行累加式、完整或更新處理的選項。  
  
-   指定在發生指定數目的錯誤之後，處理會忽略錯誤還是停止的錯誤組態。  
  
-   將輸入資料行對應至資料分割資料行。  
  
 如需處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的詳細資訊，請參閱[處理選項和設定 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
> [!NOTE]  
>  此處描述的工作不適用於 Analysis Services 表格式模型。  您無法針對表格式模型，將輸入資料行對應至資料分割資料行。 您可以改用 Analysis Services 執行 DDL 工作 ( [Analysis Services Execute DDL Task](../control-flow/analysis-services-execute-ddl-task.md) ) 來處理資料分割。  
  
## <a name="configuration-of-the-partition-processing-destination"></a>設定資料分割處理目的地  
 資料分割處理目的地會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接管理員，以連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或包含目的地所處理之 Cube 及資料分割的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。 如需詳細資訊，請參閱 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md)。  
  
 此目的地擁有一個輸入。 它不支援錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關 **[資料分割處理目的地編輯器]** 對話方塊中可設定之屬性的詳細資訊，請按一下下列主題之一：  
  
-   [資料分割處理目的地編輯器 &#40;連線管理員頁面&#41;](../partition-processing-destination-editor-connection-manager-page.md)  
  
-   [資料分割處理目的地編輯器 &#40;對應頁面&#41;](../partition-processing-destination-editor-mappings-page.md)  
  
-   [資料分割處理目的地編輯器 &#40;進階頁面&#41;](../partition-processing-destination-editor-advanced-page.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../common-properties.md)  
  
-   [資料分割處理目的地自訂屬性](partition-processing-destination-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)。  
  
  
