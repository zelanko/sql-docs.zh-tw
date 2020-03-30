---
title: Analysis Services 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 01/25/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Analysis Services
- connection managers [Integration Services], Analysis Services
- Analysis Services connection manager
ms.assetid: 9f9cadad-a1d0-4db5-98f5-df5dbbec1be4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 62e22823d19ab7dff113566927f0d59dfd4a693e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294475"
---
# <a name="analysis-services-connection-manager"></a>Analysis Services 連接管理員

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連線管理員能使套件連線到執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的伺服器，或連線到提供 Cube 和維度資料存取權的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中開發封裝時，您只能連接到 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]專案。 在執行階段，封裝會連接到您部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的伺服器和資料庫。  
  
 工作 (例如「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行 DDL」工作和「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 處理」工作) 及目的地 (例如「資料採礦模型定型」目的地) 都使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連線管理員。  
  
 如需 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的詳細資訊，請參閱[多維度模型資料庫 &#40;SSAS&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/multidimensional-model-databases-ssas)。  
  
## <a name="configuration-of-the-analysis-services-connection-manager"></a>Analysis Services 連接管理員的組態  
 當您將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連線管理員新增至套件時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立一個連線管理員 (在執行階段會解析為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連線)、設定連線管理員的屬性，並將該連線管理員新增至套件的 **Connections** 集合。 連線管理員的 **ConnectionManagerType** 屬性會設為 **MSOLAP100**。  
  
 您可以利用下列方式設定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連線管理員：  
  
-   提供一個設定為符合 Microsoft OLE Provider for Analysis Services 提供者需求的連接字串。  
  
-   指定要連接的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。  
  
-   如果您要連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體，請指定驗證模式。  

> [!NOTE]    
>  如果您在 Azure Data Factory (ADF) 中使用 SSIS，並想要連接到 Azure Analysis Services (AAS) 執行個體，您無法使用啟用 Multi-Factor Authentication (MFA) 的帳戶，而必須改用不需要任何互動功能/MFA 的帳戶或服務主體。 若要使用後者，請參閱[這裡](https://docs.microsoft.com/azure/analysis-services/analysis-services-service-principal)來建立一個並對其指派伺服器管理員角色，然後選取 [使用特定使用者名稱和密碼]  登入您連線管理員中的伺服器，最後輸入 `User name: app:YourApplicationID` 和 `Password: YourAuthorizationKey`。
  
-   指示是否在執行階段保留從連接管理員建立的連接。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [加入 Analysis Services 連線管理員對話方塊 UI 參考](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
  
