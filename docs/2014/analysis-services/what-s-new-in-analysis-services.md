---
title: 什麼&#39;新功能 Analysis Services 和 Business Intelligence |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: aa69c299-b8f4-4969-86d8-b3292fe13f08
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 33296b1b3d1935f0f716a6e411c23481ee0e2789
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356518"
---
# <a name="what39s-new-in-analysis-services-and-business-intelligence"></a>什麼&#39;新功能 Analysis Services 和 Business Intelligence
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 維持與舊版相同，但是針對多維度模型加入支援 Power View 報表的功能除外。  
  
 如需其他資訊[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]產品和技術不同，在此版本中，請參閱[What's New in SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md)。  
  
## <a name="updates-to-design-tool-installation"></a>設計工具安裝的更新  
 之前稱為 Business Intelligence Development Studio (BIDS) 的 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] for Business Intelligence (SSDT-BI) 是用來建立 Analysis Services 模型、Reporting Services 報表和 Integration Services 封裝。 您可以從以下位置下載 SSDT-BI：  
  
-   [下載 SSDT-BI for Visual Studio 2013](https://go.microsoft.com/fwlink/p/?LinkId=396526)  
  
-   [下載 SSDT-BI for Visual Studio 2012](https://go.microsoft.com/fwlink/p/?LinkID=273673)  
  
 如果電腦上已安裝舊版的 SSDT-BI 或 BIDS，較新的版本會與舊版並存安裝。 通常會在單一工作站上執行新版與舊版的設計工具，這樣一來，您就可以修改與特定伺服器版本繫結的專案和方案。  
  
> [!NOTE]  
>  Visual Studio 2012 和 Visual Studio 2013 版的 SSDT 有幾個下載網站。 大部分都未包括 BI 專案範本。 使用上述連結會讓您得到正確的版本。 您知道您擁有的是正確版本的 SSDT BI，是否您看到商業智慧專案範本資料夾。 此資料夾包含 Analysis Services、Reporting Services 和 Integration Services 適用的專案範本。 依據您安裝 SSDT-BI 的方式，您也可能會看到一個額外的 SQL Server 資料庫專案範本。  
  
 ![SSDT 中的新專案範本](media/ssdt-biprojects.png "SSDT 中的新專案範本")  
  
## <a name="features-recently-added-power-view-for-multidimensional-models"></a>最近加入的功能：多維度模型的 Power View  
 能夠針對多維度模型建立 Power View 報表的功能最先在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 1 累計更新 4 中引進。 多維度模型的 Power View 功能現在已經是 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 的一部分。  
  
 **多維度模型的 power View 報表**  
  
 ![Power View 報表](media/powerviewreport-wn.gif "Power View 報表")  
  
 此功能可幫助組織啟用要與最新用戶端報表工具一起使用的多維度模型 (也稱為 OLAP Cube)，好讓現有的 BI 投資達到最大效益。 根據多維度模型中的資料類型，使用者可以輕鬆地建立各種不同的動態視覺效果，從資料表和矩陣到泡泡圖和地圖。 多維度模型現在也支援使用 Data Analysis Expressions (DAX) 查詢。  
  
 多維度模型的 Power View 要求 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中必須有內建的 Power View 報表功能 (SharePoint 模式)。 Power View 的其他版本 (特別是 Excel 2013 中的 Power View 增益集) 不支援多維度模型。  
  
 若要進一步了解，請參閱[多維度模型的 Power View](https://msdn.microsoft.com/library/dn140246.aspx)。  
  
  
