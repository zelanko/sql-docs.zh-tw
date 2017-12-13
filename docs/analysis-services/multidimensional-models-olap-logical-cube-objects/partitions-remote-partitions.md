---
title: "遠端分割區 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- storage [Analysis Services], partitions
- archiving remote partitions [Analysis Services]
- partitions [Analysis Services], remote
- restoring remote partitions [Analysis Services]
- backing up remote partitions [Analysis Services]
- partitions [Analysis Services], storage
- storing data [Analysis Services], partitions
- MasterDataSourceID property
- remote partitions [Analysis Services]
ms.assetid: 63f5d9f5-c6b6-4ceb-94fe-7b6c396d10bb
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3ed594520b84d2e45f9729f90f188a1964484a17
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="partitions---remote-partitions"></a>資料分割-遠端資料分割
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]遠端分割區資料會儲存在 Microsoft 的不同執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]比包含資料分割和其父 cube 的定義 （中繼資料） 的執行個體。 遠端資料分割是在與定義資料分割和其父 Cube 的相同 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上進行管理。  
  
> [!NOTE]  
>  若要儲存遠端資料分割，電腦必須擁有的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]安裝並執行相同的 service pack 層級與資料分割定義所在的執行個體。 而舊版 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的遠端資料分割則不予支援。  
  
 量值群組中包含遠端資料分割時，會將 Cube 的記憶體和 CPU 使用情形分散在該量值群組的所有資料分割中。 例如，單獨或當成父 Cube 處理的一部分來處理遠端資料分割時，該資料分割的大多數記憶體和 CPU 使用是發生在遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上。  
  
> [!NOTE]  
>  包含遠端資料分割的 Cube 可以包含啟用寫入的維度。不過，這可能會影響 Cube 的效能。 如需啟用寫入的維度的詳細資訊，請參閱[Write-Enabled 維度](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)。  
  
## <a name="storage-modes-for-remote-partitions"></a>遠端資料分割的儲存模式  
 遠端資料分割可以使用本機資料分割所使用的任何儲存類型：多維度 OLAP (MOLAP)、混合式 OLAP (HOLAP) 或關聯式 OLAP (ROLAP)。 遠端資料分割也可以使用主動式快取。 依遠端資料分割的儲存模式而定，下列資料是儲存在遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上。  
  
|||  
|-|-|  
|儲存類型|data|  
|MOLAP|資料分割的彙總，以及資料分割之來源資料的副本。|  
|HOLAP|資料分割的彙總|  
|ROLAP|無資料分割資料|  
  
 如果量值群組包含多個儲存在多個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的 MOLAP 或 HOLAP 資料分割，則 Cube 會將量值群組的資料分散到那些 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之間。  
  
## <a name="merging-remote-partitions"></a>合併遠端資料分割  
 遠端資料分割只可與儲存在相同遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的其他遠端資料分割合併。 如需有關合併資料分割的詳細資訊，請參閱[Analysis Services &#40; 中的 合併資料分割SSAS-多維度 &#41;](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md).  
  
## <a name="archiving-and-restoring-remote-partitions"></a>封存與還原遠端資料分割  
 封存或還原用來儲存遠端資料分割的資料庫時，可封存或還原遠端資料分割中的資料。 如果您還原資料庫，而未還原遠端資料分割，則必須先處理遠端資料分割後，才可使用該資料分割中的資料。 如需有關封存與還原資料庫的詳細資訊，請參閱[備份與還原的 Analysis Services 資料庫](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)。  
  
## <a name="see-also"></a>請參閱  
 [建立及管理遠端分割區 &#40;Analysis Services &#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)   
 [處理 Analysis Services 物件](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md)  
  
  
