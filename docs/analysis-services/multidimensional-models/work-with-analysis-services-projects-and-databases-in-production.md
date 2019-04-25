---
title: 使用 Analysis Services 專案和在生產環境中的資料庫 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f90af41c397da20fb26c73bebc6723b9a3cf6270
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743234"
---
# <a name="work-with-analysis-services-projects-and-databases-in-production"></a>使用 Analysis Services 專案和在生產環境中的資料庫
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  當您已經從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫開發並部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之後，您必須決定要如何變更已部署之資料庫中的物件。 某些變更 (例如，與安全性角色、資料分割和儲存設定有關的變更) 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]來進行， 其他變更則只能在專案模式或線上模式中，使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]來進行 (例如，加入屬性或使用者自訂階層)。  
  
 一旦在線上模式中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 變更已部署的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 資料庫之後，之前用於部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案就會過期。 如果開發人員在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中進行任何變更，而且嘗試部署這個修改過的專案，則會出現一則提示，提醒開發人員將會覆寫整個資料庫。 如果開發人員要覆寫整個資料庫，也必須處理這個資料庫； 當這些變更是由實際執行人員直接針對已部署的資料庫進行，而且並未與開發小組溝通時，這個問題會變得相當複雜，因為這些人員將不會了解為何他們所做的變更不再出現在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中。  
  
 您可使用 SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工具中提供的幾個方法來避免這個情況所產生的問題。  
  
-   方法 1:每當變更的實際執行版本[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫，請使用[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]來建立新的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案為基礎的修改版本[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。 這個新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案可以當作專案的主要副本簽入到原始檔控制系統中。 不論是在線上模式中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 對 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 資料庫進行變更，這個方法都一樣有效。  
  
-   方法 2：只有進行變更的實際執行版本[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]在專案模式中。 在使用這個方法時，可以使用 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 中提供的選項來保留 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]所做的變更 (例如，安全性角色和儲存設定)。 如此可確保與設計有關的設定會保留在專案檔案中 (可以忽略儲存設定和安全性角色)，而且儲存設定和安全性角色會使用線上伺服器。  
  
-   方法 3:只有進行變更的實際執行版本[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]在線上模式中。 因為這兩個工具只能與相同的線上伺服器一起運作，所以不可能會有未同步的不同版本。  
  
  
