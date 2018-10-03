---
title: 表格式模型 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 11a5a9332c7fa85fd6407523ffd9c7c48a2c0514
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198748"
---
# <a name="tabular-modeling-ssas-tabular"></a>表格式模型化 (SSAS 表格式)
  表格式模型是 Analysis Services 的記憶體中資料庫。 xVelocity 記憶體中分析引擎 (VertiPaq) 採用最先進的壓縮演算法和多執行緒查詢處理器，可透過 Microsoft Excel 和 Microsoft [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 等報表用戶端應用程式快速存取表格式模型物件和資料。  
  
 表格式模型支援兩種模式的資料存取：快取模式和 DirectQuery 模式。 在快取模式中，您可以整合來自多個來源的資料，包括關聯式資料庫、資料摘要及一般文字檔。 在 DirectQuery 模式，您可以略過記憶體中模型，讓用戶端應用程式可以直接在 (SQL Server 關聯式) 來源中查詢資料。  
  
 您可以使用新的表格式模型專案範本，在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中撰寫表格式模型。 您可以從多個來源匯入資料，然後透過加入關聯性、導出資料行、量值、KPI 及階層，來充實模型。 接著可將模型部署至 Analysis Services 的執行個體，再由其中的用戶端報表應用程式連接至模型。 您可以在 SQL Server Management Studio 中管理已部署的模型，就像是管理多維度模型一樣。 您也可以對其進行資料分割以最佳化處理，並使用以角色為基礎的安全性提供資料列層級的安全性。  
  
## <a name="in-this-section"></a>本節內容  
 [表格式模型方案&#40;SSAS 表格式&#41;](../tabular-model-solutions-ssas-tabular.md)  
  
 [表格式模型資料庫&#40;SSAS 表格式&#41;](tabular-model-databases-ssas-tabular.md)  
  
 [表格式模型資料存取](tabular-model-data-access.md)  
  
  
