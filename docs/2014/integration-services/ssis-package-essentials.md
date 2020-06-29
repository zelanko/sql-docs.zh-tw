---
title: SSIS 套件基本概念 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- package requirements
ms.assetid: b0c86c35-e3d3-4724-9a96-4087e9d74bf3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2c4e3f6637c4e9fd65b0218b8489372355b3608f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421046"
---
# <a name="ssis-package-essentials"></a>SSIS 封裝基本功能
  封裝是實作 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 功能以擷取、轉換和載入資料的物件。 您可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 中使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]設計師來建立封裝。 您也可以執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 匯入和匯出精靈或 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 連接專案精靈來建立封裝。 如需詳細資訊，請在 SSIS 設計師的[SQL Server Data Tools 中建立封裝](create-packages-in-sql-server-data-tools.md)和匯[入專案嚮導](../../2014/integration-services/import-project-wizard.md)。  
  
 基本的套件包含下列項目：  
  
 **控制流程元素**  
 這些必要的元素可執行多種功能、提供結構，並控制元素執行的順序。 主要的控制流程元素為工作、容器和優先順序條件約束。 封裝中至少要有一個控制流程元素。  
  
 如需詳細資訊，請參閱 [控制流程](control-flow/control-flow.md)。  
  
 **資料流程元素**  
 這些選擇性的元素會擷取資料、修改資料並將資料載入資料來源。 主要資料流程元素為來源、轉換及目的地。 封裝中不必有任何資料流程元素。  
  
 如需詳細資訊，請參閱 [資料流程](data-flow/data-flow.md)。  
  
 如需如何建立基本封裝的範例，請參閱[第1課：建立專案和基本封裝](lesson-1-create-a-project-and-basic-package-with-ssis.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [在 SQL Server 資料工具中建立封裝](create-packages-in-sql-server-data-tools.md)  
  
-   [在控制流程中加入或刪除工作或容器](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
-   [設定工作或容器的屬性](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
-   [在資料流程中加入或刪除元件](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
## <a name="related-content"></a>相關內容  
  
1.  MSDN.Microsoft.com 上的影片： [建立基本封裝 (SQL Server 影片)](https://go.microsoft.com/fwlink/?LinkId=131023)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 封裝](../../2014/integration-services/integration-services-ssis-packages.md)   
 [優先順序條件約束](control-flow/precedence-constraints.md)  
  
  
