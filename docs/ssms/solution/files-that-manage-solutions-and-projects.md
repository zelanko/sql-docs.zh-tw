---
title: "管理方案和專案的檔案 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- projects [SQL Server Management Studio], files
- .ssmssln files
- .ssmsmobileproj files
- .ssmsasproj files
- .ssmssqlproj files
- .sqlsuo files
- files [SQL Server Management Studio], projects
ms.assetid: e19d2859-0b97-4727-ac27-c4c226d86b2f
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 13c811a0c616a9ef859e86c688804c829ec0d9f0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="files-that-manage-solutions-and-projects"></a>管理方案和專案的檔案
 <a name="-this-topic-describes-the-file-types-that-are-specific-to-includemsconameincludesmsconamemdmd-includessmanstudiofullincludesssmanstudiofullmdmd-by-default-all-solutions-and-their-projects-are-created-in-my-documentssql-server-management-studio-projects"></a>-此主題說明 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 專用的檔案類型。 依預設，所有方案及其專案都建立在 \My Documents\SQL Server Management Studio Projects 中。  
 -  
 -## Management Studio 解決方案檔案  
 -[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 使用不同於 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] 或 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual Studio 的檔案類型。 這代表您無法在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 Visual Studio 中開啟 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] 方案。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 方案檔可讓方案總管顯示一個用以管理檔案的圖形介面。  
 -  
 -|延伸模組|檔案類型|說明|建立者|  
 -|-------------|-------------|---------------|--------------|  
 -|.ssmssln|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 方案物件|提供參考 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 專案、專案項目和方案之磁碟位置的環境|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]|  
 -  
 -## Management Studio 專案檔案  
 -專案會依照與解決方案包含解決方案檔案 (用來管理解決方案中的物件) 相同的方式來包含專案檔案。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 針對專案所建立之專案檔的類型，會隨著用來建立專案的範本而不同。 下表說明針對每個專案所建立之檔案的類型。  
 -  
 -|延伸模組|專案範本|  
 -|-------------|--------------------|  
 -|.ssmssqlproj|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 指令碼專案|  
 -|.ssmsasproj|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] 指令碼專案|  
 -  
 -## 解決方案層級檔案的位置  
 -根據預設，解決方案層級檔案會建立在第一個以解決方案建立之專案的實體目錄中。 您可以建立一個方案來指定方案的目錄，也可以在建立新專案時指定目錄。  
 -  
 -若目錄結構類似於方案總管中所顯示的邏輯結構，專案和解決方案檔案就會較容易尋找，也較容易與小組的其他開發人員共用。  
 -  
 -## 另請參閱  
 -[利用編碼管理檔案](../../ssms/solution/manage-files-with-encoding.md)  
 -[其他檔案](../../ssms/solution/miscellaneous-files.md)  
 -[方案總管](../../ssms/solution/solution-explorer.md)  
 -[解決方案 &#40;SQL Server Management Studio&#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
 -[專案 &#40;SQL Server Management Studio&#41;](../../ssms/solution/projects-sql-server-management-studio.md)  
 -[方案總管原始檔控制](https://msdn.microsoft.com/en-us/library/ms173879.aspx)  
  
