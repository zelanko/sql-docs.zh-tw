---
title: Analysis Services 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Analysis Services
- connection managers [Integration Services], Analysis Services
- Analysis Services connection manager
ms.assetid: 9f9cadad-a1d0-4db5-98f5-df5dbbec1be4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8f8ca9ce77e151e761e2cbb1f9128a44784af8ca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68890396"
---
# <a name="analysis-services-connection-manager"></a>Analysis Services 連接管理員
  連接管理員可讓封裝連接到執行[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫的伺服器，或是連接到提供 cube 和[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]維度資料存取權的專案。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中開發封裝時，您只能連接到 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]專案。 在執行階段，封裝會連接到您部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的伺服器和資料庫。  
  
 工作 (例如「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行 DDL」工作和「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 處理」工作) 及目的地 (例如「資料採礦模型定型」目的地) 都使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連線管理員。  
  
 如需 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的詳細資訊，請參閱[多維度模型資料庫 &#40;SSAS&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/multidimensional-model-databases-ssas)。  
  
## <a name="configuration-of-the-analysis-services-connection-manager"></a>Analysis Services 連接管理員的組態  
 當您[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]將連線管理員加入封裝時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]會建立在執行時間解析為[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]連接的連線管理員、設定連線管理員屬性，並將連線管理員加入封裝上`Connections`的集合。 連接管理員的 `ConnectionManagerType` 屬性會設為 `MSOLAP100`。  
  
 您可以利用下列方式設定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連線管理員：  
  
-   提供一個設定為符合 Microsoft OLE Provider for Analysis Services 提供者需求的連接字串。  
  
-   指定要連接的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。  
  
-   如果您要連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體，請指定驗證模式。  
  
-   指示是否在執行階段保留從連接管理員建立的連接。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [加入 Analysis Services 連接管理員對話方塊 UI 參考](add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
  
