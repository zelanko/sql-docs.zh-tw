---
title: 管理方案和專案的檔案 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], files
- .ssmssln files
- .ssmsmobileproj files
- .ssmsasproj files
- .ssmssqlproj files
- .sqlsuo files
- files [SQL Server Management Studio], projects
ms.assetid: e19d2859-0b97-4727-ac27-c4c226d86b2f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6e8481c1cce3e43287c04678ddae10ac1b0703af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63044349"
---
# <a name="files-that-manage-solutions-and-projects"></a>管理方案和專案的檔案
  本主題描述特有[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的檔案類型。 依預設，所有方案及其專案都建立在 \My Documents\SQL Server Management Studio Projects 中。  
  
## <a name="management-studio-solution-files"></a>Management Studio 方案檔  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]使用與[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]或[!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 不同的檔案類型。 這代表您無法在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Visual Studio 中開啟 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 方案。 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 方案檔可讓方案總管顯示一個用以管理檔案的圖形介面。  
  
|分機|檔案類型|描述|建立者|  
|---------------|---------------|-----------------|----------------|  
|.ssmssln|
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 方案物件|為環境提供專案、專案專案和方案之[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]磁片位置的參考|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
  
## <a name="management-studio-project-files"></a>Management Studio 專案檔  
 專案依照方案包含方案檔 (用來管理方案中的物件) 的相同方式來包含專案檔。 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 針對專案所建立之專案檔的類型，會隨著用來建立專案的範本而不同。 下表說明針對每個專案所建立之檔案的類型。  
  
|分機|專案範本|  
|---------------|----------------------|  
|.ssmssqlproj|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令碼專案|  
|.ssmsasproj|
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 指令碼專案|  
  
## <a name="location-of-solution-level-files"></a>方案層級檔案的位置  
 依預設，方案層級的檔案是建立在方案所建立的第一個專案之實體目錄中。 您可以建立一個方案來指定方案的目錄，也可以在建立新專案時指定目錄。  
  
 如果目錄結構類似於 [方案總管] 所顯示的邏輯結構，專案和方案檔會比較容易尋找，團隊的其他開發人員也比較容易共用它們。  
  
## <a name="see-also"></a>另請參閱  
 [以編碼管理檔案](manage-files-with-encoding.md)   
 [其他檔案](miscellaneous-files.md)   
 [方案總管](solution-explorer.md)   
 [解決方案 &#40;SQL Server Management Studio&#41;](solutions-sql-server-management-studio.md)   
 [專案 &#40;SQL Server Management Studio&#41;](projects-sql-server-management-studio.md)   
 [方案總管原始檔控制](../../database-engine/solution-explorer-source-control.md)  
  
  
