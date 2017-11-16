---
title: "多維度模型資料庫 (SSAS) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [Analysis Services], databases
- SQL Server Analysis Services, databases
- SSAS, databases
- Analysis Services, databases
- databases [Analysis Services], designing
- Business Intelligence Development Studio, databases [Analysis Services]
- databases [Analysis Services]
ms.assetid: 78b2f22a-b7bd-4a2b-b6fc-0bff4d2b3168
caps.latest.revision: 55
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2b9b4fa79c4ef7a37158c1fbeea32a80c56effa2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="multidimensional-model-databases-ssas"></a>多維度模型資料庫 (SSAS)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫是資料來源、資料來源檢視、Cube、維度及角色的集合。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫也可以包含資料採礦結構，以及提供您方法將使用者定義函數加入至資料庫的自訂組件。  
  
 Cube 是 Analysis Services 的基本查詢物件。 當您透過用戶端應用程式連接至 Analysis Services 資料庫時，您可以連接至該資料庫內的 Cube。 如果跨多個內容重複使用維度、組件、角色或採礦結構，資料庫可能包含多個 Cube。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 您可以程式設計方式或透過下列其中一個互動方法，建立及修改  資料庫：  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案部署到指定的  執行個體。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 這個程序會建立  資料庫 (如果該執行個體中尚未存在這個名稱的資料庫)，並將新建之資料庫內的已設計物件具現化。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫時，對於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中物件所做的變更必須要在專案部署到  執行個體之後，才會生效。  
  
-   請使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]於 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 執行個體內建立空的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]資料庫，然後使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 直接連接到該資料庫，並在其中建立物件 (而不是在專案內建立)。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 當以這個方式使用  資料庫時，對物件所做的變更會在儲存已變更的物件之後，於您所連接的這個資料庫中生效。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會使用與原始檔控制軟體的整合，以支援多位開發人員同時在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中使用不同的物件。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 開發人員也可以直接與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫互動，而不用透過 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，但是這樣做會有一個風險，就是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中的物件可能不會與用於部署的  專案同步。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在部署之後，您會使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來管理  資料庫。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫進行某些變更 (如資料分割和角色的變更)，而這樣也會使得 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中的物件不會與用於部署的  專案同步。  
  
## <a name="related-tasks"></a>相關工作  
 [附加和卸離 Analysis Services 資料庫](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
 [備份與還原 Analysis Services 資料庫](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
 [記錄和編寫 Analysis Services 資料庫的指令碼](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
 [修改或刪除 Analysis Services 資料庫](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)  
  
 [移動 Analysis Services 資料庫](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)  
  
 [重新命名多維度資料庫 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/rename-a-multidimensional-database-analysis-services.md)  
  
 [多維度資料庫的相容性層級 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)  
  
 [設定多維度資料庫屬性 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)  
  
 [同步處理 Analysis Services 資料庫](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)  
  
 [在 ReadOnly 和 ReadWrite 模式之間切換 Analysis Services 資料庫](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
## <a name="see-also"></a>請參閱＜  
 [在連線模式下連接至 Analysis Services 資料庫](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)   
 [建立 Analysis Services 專案 &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)   
 [使用 MDX 查詢多維度資料](../../analysis-services/multidimensional-models/mdx/querying-multidimensional-data-with-mdx.md)  
  
  

