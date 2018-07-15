---
title: 相容性層級 (SSAS 表格式 SP1) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: 8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d4c04690906d9b5f3fd38ddf444d6c3f99e917a9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37298998"
---
# <a name="compatibility-level-ssas-tabular-sp1"></a>相容性層級 (SSAS 表格式 SP1)
  您可以指定*相容性層級*建立新的表格式模型專案、 升級現有的表格式模型專案、 升級部署的表格式模型資料庫，或匯入 PowerPivot 活頁簿時。  
  
## <a name="compatibility-level"></a>相容性層級  
 將新版本和 Service Pack 安裝到實際作業電腦上之前，通常會先安裝到開發和測試電腦上。 在這類情況下，務必了解為新的以及已部署到生產環境的表格式模型專案設定相容性層級的重要。  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Analysis Services 執行個體支援下列相容性層級 (資料庫版本)：  
  
-   SQL Server 2012 (1100)  
  
-   SQL Server 2012 SP1 (1103)  
  
-   SQL Server 2014 (1103)  
  
### <a name="set-compatibility-level-when-creating-a-new-tabular-model-project"></a>在建立新的表格式模型專案時設定相容性層級  
 在建立新的表格式模型專案中 SQL Server Data Tools (SSDT)，當**新表格式專案選項**對話方塊，您可以指定相容性層級。 您可以選擇建立要部署到 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更新版本 Analysis Services 執行個體或部署到 SQL Server 2012 Analysis Services 執行個體 (不含 Service Pack 1) 的新專案。  
  
 您也可以透過選取 **[不要再顯示此訊息]** 選項指定預設相容性層級。 所有後續專案都將使用您指定的相容性層級。 您可以在 SSDT 的 [選項] 中變更預設相容性層級。  
  
### <a name="upgrade-an-existing-tabular-model-project-to-1103-compatibility-level"></a>將現有的表格式模型專案升級至 1103 相容性層級  
 您可以升級表格式模型專案，再安裝 SSDT 中建立[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]或更新版本，才能使用，成為資料庫版本 1103年相容**相容性層級**模型中的屬性**屬性**視窗。 為了升級表格式模型專案，安裝 SSDT 所在的電腦必須已安裝 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更新版本，而工作空間資料庫所在的 Analysis Services 執行個體同樣必須已安裝 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更新版本。 您無法降級為舊版。  
  
### <a name="upgrade-a-deployed-tabular-model-database-to-1103-compatibility-level"></a>將已部署的表格式模型資料庫升級至 1103 相容性層級  
 您可以使用，以升級現有部署的表格式模型資料庫版本 1103 相容的 SQL Server Management Studio (SSMS)**相容性層級**屬性中的**資料庫屬性**. 為了進行升級，安裝 SQL Server Analysis Services 執行個體所在的電腦上必須已安裝 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更新版本。 您無法將部署的表格式模型資料庫降級為舊版。  
  
### <a name="import-from-powerpivot"></a>從 PowerPivot 匯入  
 透過從 PowerPivot 匯入來建立新的表格式模型專案時，可以指定要將相容性層級升級為預設相容性層級 (之前已在 SSDT 中設定的話)，或是維持 PowerPivot 活頁簿中已指定的相容性層級。  
  
### <a name="check-compatibility-level-for-a-tabular-model-database-in-ssms"></a>在 SSMS 中檢查表格式模型資料庫的相容性層級  
 您可以藉由檢視檢查在 SSMS 中表格式模型資料庫的相容性層級**相容性層級**屬性 (新功能[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) 中**資料庫屬性**。  
  
### <a name="check-supported-compatibility-level-for-an-analysis-services-instance-in-ssms"></a>在 SSMS 中檢查 Analysis Services 執行個體支援的相容性層級  
 您可以檢查支援的相容性層級，在 SSMS 中藉由檢視**支援的相容性層級**屬性上的**資訊**頁面 (新功能[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]) 中**分析服務內容**。 支援的相容性層級 1103 表示已安裝 SQL Server SP1 或更新版本。 支援的相容性層級無法變更。  
  
  
