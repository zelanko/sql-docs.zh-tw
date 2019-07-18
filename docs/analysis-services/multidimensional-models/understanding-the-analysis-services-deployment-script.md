---
title: 了解 Analysis Services 部署指令碼 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 84179762d2c4819fb5fc5f82ad6d0528ea689ecf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208444"
---
# <a name="understanding-the-analysis-services-deployment-script"></a>了解 Analysis Services 部署指令碼
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 產生的 XMLA 部署指令碼包含兩個區段：  
  
-   部署指令碼的第一個部分包含要建立、改變或刪除目的地資料庫中的適當 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件時所需的命令。 根據預設， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案產生的輸入檔是以累加部署為基礎。 因此，XMLA 部署指令碼將只會影響已變更或刪除的物件。  
  
-   部署指令碼的第二個部分包含僅要處理目的地伺服器上所建立或改變的物件時所需的命令 ([處理預設] 選項) 或完整處理目的地資料庫時所需的命令。 您也可以選擇讓部署指令碼不包含任何處理命令。  
  
 整個部署指令碼可在單一交易或多筆交易中執行。 如果指令碼在多筆交易中執行，指令碼的第一個部分會以單一交易執行，而每一個物件會在它自己的交易中處理。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈只會將物件部署到單一 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中。 它不會部署任何伺服器層級的物件或資料。  
  
## <a name="see-also"></a>另請參閱  
 [執行 Analysis Services 部署精靈](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [了解用來建立部署指令碼的輸入檔](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)  
  
  
