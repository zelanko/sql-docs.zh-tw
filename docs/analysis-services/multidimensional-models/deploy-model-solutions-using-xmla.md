---
title: 使用 XMLA 部署模型方案 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ce0f50d158d715ddbbc689c47a012a4e92ba7c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208960"
---
# <a name="deploy-model-solutions-using-xmla"></a>使用 XMLA 部署模型方案
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，[編寫資料庫的指令碼為]  命令的 [CREATE 至]  選項會建立整個 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫或其中一個構成物件的 XML 指令碼。 產生的指令碼可在另一部電腦上執行，來重建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的結構描述 (中繼資料)。 此指令碼會產生整個資料庫，而且使用此指令碼時，沒有可累加更新已部署物件的機制。 執行指令碼及部署資料庫之後，必須先加以處理，使用者才可以瀏覽新建的資料庫。  
  
 如需 [編寫資料庫的指令碼為]  命令的詳細資訊，請參閱[記錄和編寫 Analysis Services 資料庫的指令碼](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)。  
  
## <a name="modifying-object-properties-in-the-xml-script"></a>在 XML 指令碼中修改物件屬性  
 使用 [編寫資料庫的指令碼為]  命令時，您不能修改資料庫物件的特定屬性 (例如資料庫名稱、資料來源連接字串和安全性設定)。 這些屬性必須在產生指令碼之後，於指令碼中手動修改；或在執行指令碼之後，在已部署的資料庫中加以修改。  
  
> [!IMPORTANT]  
>  如果您針對資料來源或模擬目的在連接字串中指定密碼，XML 指令碼將不會包含這項資訊。 由於在這種狀況下需要使用密碼進行處理，所以您必須在 XML 指令碼執行之前手動加入密碼，或在 XML 指令碼執行之後加入密碼。  
  
## <a name="see-also"></a>另請參閱  
 [Deploy Model Solutions Using the Deployment Wizard](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)   
 [同步處理 Analysis Services 資料庫](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)  
  
  
