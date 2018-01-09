---
title: "移動資料採礦物件 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], models
- data mining editor [Analysis Services]
- mining models [Analysis Services], managing
- Data Mining Designer
- mining models [Analysis Services], modifying
ms.assetid: bc108407-2603-4387-b930-b5bb9df78069
caps.latest.revision: "45"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c43da2044b4f3231d947c88626cb43081fb29f6a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="moving-data-mining-objects"></a>移動資料採礦物件
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]移動資料採礦物件最常見的案例是要部署到生產環境中，從測試或分析環境的模型，或與其他使用者共用模型。  
  
 本主題描述如何使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供的工具和指令碼語言來移動資料採礦物件。  
  
## <a name="moving-data-mining-objects-between-databases-or-servers"></a>在資料庫或伺服器之間移動資料採礦物件  
 您可以透過以下方法在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫之間或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之間移動資料採礦物件：  
  
-   將方案重新部署到至其他資料庫。  
  
-   撰寫個別物件的指令碼。  
  
-   備份與還原資料庫副本。  
  
-   匯出和匯入結構與模型。  
  
 下節詳細說明這些選項。  
  
### <a name="deploying"></a>部署  
 需要有使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 建立的方案檔，才能將方案部署至不同的伺服器或資料庫。  
  
 如需部署 Analysis Services 方案的詳細資訊，請參閱[部署 Analysis Services 專案 &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)。  
  
### <a name="scripting"></a>指令碼  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供了數種語言，可用於編寫物件的指令碼。  
  
-   **XMLA**：您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中以滑鼠右鍵按一下物件，使用 XMLA 編寫物件的指令碼。 若要執行指令碼，請在目標伺服器上的 [XMLA 查詢] 視窗中開啟指令碼。  
  
-   **DMX**：您可以透過使用範本或 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中提供的其中一個查詢產生器建立指令碼。  
  
 但請注意，各指令碼語言可執行的工作之間有些差異：  
  
-   諸如物件描述和資料繫結等屬性只能透過 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 語言來建立或變更，無法透過 DMX。  
  
-   只有 DMX 支援匯入和匯出採礦物件。  
  
-   只有 DMX 支援產生 PMML 或從 PMML 匯入模型定義。  
  
-   只有 DMX 支援使用應用程式資料來定型模型。 此外，DMX INSERT INTO 陳述式支援在不提供索引鍵資料行值的情況下進行模型定型。  
  
 如需詳細資訊，請參閱[使用 Analysis Services 指令碼語言 &#40;ASSL&#41; 開發](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。  
  
### <a name="backup-and-restore"></a>備份與還原  
 備份和還原整個 Analysis Services 資料庫是絕佳的方法 (如果您的資料採礦方案相依於 OLAP 物件的話)。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 提供備份和還原功能，讓資料庫備份更快速而且更方便。  
  
 如需備份的詳細資訊，請參閱 [備份與還原 Analysis Services 資料庫](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)。  
  
### <a name="exporting-and-importing"></a>匯出和匯入  
 利用 DMX 陳述式匯出採礦模型與結構，然後重新匯入，是移動或備份個別關聯式資料採礦物件最方便的方式。 如需有關這些作業之 DMX 語法的詳細資訊，請參閱下列主題：  
  
-   [EXPORT &#40;DMX&#41;](../../dmx/export-dmx.md)  
  
-   [IMPORT &#40;DMX&#41;](../../dmx/import-dmx.md)  
  
 如果您指定了 INCLUDE DEPENDENCIES 選項， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也會匯出任何所需資料來源檢視的定義，而且當您匯入模型或結構時，它將在目標伺服器上重新建立資料來源檢視。 在您已經完成匯入模型的作業之後，請務必針對此物件設定必要的採礦權限。  
  
> [!NOTE]  
>  您無法使用 DMX 來匯出和匯入 OLAP 模型。 如果採礦模型是以 OLAP Cube 為基礎，您必須使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所提供的功能來備份和還原整個資料庫，或重新部署 Cube 及其模型。  
  
## <a name="see-also"></a>請參閱  
 [資料採礦方案與物件的管理](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md)  
  
  
