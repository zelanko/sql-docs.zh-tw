---
title: 什麼&#39;適用於 SQL Server 2014 報表產生器的新功能 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8223c19b-4b0d-4b1d-a042-9a726c18e708
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 15e4e4a90232f4db1b83b3a09d45589e6fcdeb8d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48226878"
---
# <a name="what39s-new-in-report-builder-for-sql-server-2014"></a>什麼&#39;適用於 SQL Server 2014 報表產生器的新功能
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 導入了許多 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能。  
  
 如需功能在此版本中的其他資訊[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]產品和技術，請參閱[What's New in SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md)。  
  
> [!TIP]  
>  如最新的資訊以及有關此版本中的新功能的資源，請參閱[在 SQL Server Reporting Services (SSRS) 的新功能的其他資訊](http://go.microsoft.com/fwlink/?LinkId=207147)。  
  
##  <a name="ExcelRenderer"></a> 適用於 Microsoft Excel 2007-2010 和 Microsoft Excel 2003 的 excel 轉譯器  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Excel 轉譯延伸模組是 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 新功能，它會將報表轉譯為相容於 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 2007-2010 以及已安裝 Microsoft Office Word、Excel 和 PowerPoint 相容性套件的 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 2003 的 Excel 文件。 此格式為 Office Open XML，其副檔名為 .xlsx。  
  
 此 Excel 轉譯延伸模組移除了舊版的限制，可與 Excel 2003 相容。 以下列出轉譯延伸模組中的改進功能：  
  
-   每個工作表的資料列上限為 1,048,576。  
  
-   每個工作表的資料行上限為 16,384。  
  
-   工作表中允許的色彩數目約為 1600 萬 (24 位元色彩)。  
  
-   ZIP 壓縮提供較小的檔案大小。  
  
 如需詳細資訊，請參閱[匯出至 Microsoft Excel &#40;報表產生器及 SSRS&#41;](report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)。  
  
##  <a name="WordRenderer"></a> Microsoft Word 2007-2010 和 Microsoft Word 2003 的 Word 轉譯器  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Word 轉譯延伸模組是 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 的新功能，它會將報表轉譯為相容於 [!INCLUDE[ofprword](../includes/ofprword-md.md)] 2007-2010 以及已安裝 [!INCLUDE[ofprword](../includes/ofprword-md.md)] Office Word、Excel 和 PowerPoint 相容性套件的 [!INCLUDE[msCoName](../includes/msconame-md.md)] 2003 的 Word 文件。 此格式為 Office Open XML，其副檔名為 docx。  
  
 除了讓 Word 2007-2010 新功能用於匯出的報表之外，匯出的報表 *.docx 檔案通常較小。 使用 Word 轉譯器所匯出的報表通常比使用 Word 2003 轉譯器所匯出的相同報表小得多。  
  
 如需詳細資訊，請參閱[匯出至 Microsoft Word &#40;報表產生器及 SSRS&#41;](report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 中的報表產生器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
