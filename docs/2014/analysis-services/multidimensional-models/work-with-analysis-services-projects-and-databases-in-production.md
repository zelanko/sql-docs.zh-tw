---
title: 使用 Analysis Services 專案和在生產環境中的資料庫 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, projects
ms.assetid: c589097f-ad29-4b97-8c7e-b8a910909c1a
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a28d61cd262fb348e839055ea0f0d443187bf75
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37302798"
---
# <a name="working-with-analysis-services-projects-and-databases-in-a-production-environment"></a>在實際執行環境中搭配 Analysis Services 專案及資料庫使用
  當您已經從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫開發並部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之後，您必須決定要如何變更已部署之資料庫中的物件。 某些變更 (例如，與安全性角色、資料分割和儲存設定有關的變更) 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]來進行， 其他變更則只能在專案模式或線上模式中，使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]來進行 (例如，加入屬性或使用者自訂階層)。  
  
 一旦在線上模式中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 變更已部署的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 資料庫之後，之前用於部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案就會過期。 如果開發人員在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中進行任何變更，而且嘗試部署這個修改過的專案，則會出現一則提示，提醒開發人員將會覆寫整個資料庫。 如果開發人員要覆寫整個資料庫，也必須處理這個資料庫； 當這些變更是由實際執行人員直接針對已部署的資料庫進行，而且並未與開發小組溝通時，這個問題會變得相當複雜，因為這些人員將不會了解為何他們所做的變更不再出現在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中。  
  
 您可使用 SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工具中提供的幾個方法來避免這個情況所產生的問題。  
  
-   方法 1：每當對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的實際執行版本進行變更時，請使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 來根據修改過的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫版本建立新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。 這個新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案可以當作專案的主要副本簽入到原始檔控制系統中。 不論是在線上模式中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 對 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 資料庫進行變更，這個方法都一樣有效。  
  
-   方法 2：在專案模式中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，僅針對 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 資料庫的實際執行版本進行變更。 在使用這個方法時，可以使用 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 中提供的選項來保留 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]所做的變更 (例如，安全性角色和儲存設定)。 如此可確保與設計有關的設定會保留在專案檔案中 (可以忽略儲存設定和安全性角色)，而且儲存設定和安全性角色會使用線上伺服器。  
  
-   方法 3：在線上模式中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，僅針對 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 資料庫的實際執行版本進行變更。 因為這兩個工具只能與相同的線上伺服器一起運作，所以不可能會有未同步的不同版本。  
  
  
