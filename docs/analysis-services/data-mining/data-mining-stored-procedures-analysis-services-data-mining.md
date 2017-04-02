---
title: "資料採礦預存程序 (Analysis Services - 資料採礦) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "預存程序 [Analysis Services], 資料採礦"
ms.assetid: a751856d-33bd-4788-9593-317b2826132d
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 26
---
# 資料採礦預存程序 (Analysis Services - 資料採礦)
  從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可支援以任何 Managed 語言所撰寫的預存程序。 支援的 Managed 語言包括 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET、C# 和 Managed C++。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，您可以使用 **CALL** 陳述式直接呼叫預存程序，或是當作資料採礦延伸模組 (DMX) 查詢的一部分來呼叫。  
  
 如需呼叫 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 預存程序的詳細資訊，請參閱[呼叫預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)。  
  
 如需 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 可程式性的一般資訊，請參閱[資料採礦程式設計](../../analysis-services/data-mining-programming.md)。  
  
 如需如何撰寫資料採礦物件之程式的其他資訊，請參閱 MSDN Library 中的文件 [SQL Server Data Mining Programmability](http://go.microsoft.com/fwlink/?LinkId=93735) (SQL Server 資料採礦可程式性)。  
  
> [!NOTE]  
>  當您查詢採礦模型，尤其是當您測試新的資料採礦方案時，您可能會發現呼叫由資料採礦引擎在內部使用的系統預存程序是很方便的事情。 您可以檢視這些系統預存程序的名稱，其方式是使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器上建立追蹤，然後建立、瀏覽及查詢資料採礦模型。 但是，[!INCLUDE[msCoName](../../includes/msconame-md.md)] 不保證系統預存程序在不同版本之間的相容性，而且您絕對不能在實際系統中使用系統預存程序的呼叫。 為了提供相容性，您應該改用 DMX 或 XML/A 來建立自己的查詢。  
  
## 本節內容  
  
-   [SystemGetCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
## 參考  
 [在 Analysis Services 中編寫管理工作的指令碼](../../analysis-services/instances/script-administrative-tasks-in-analysis-services.md)  
  
## 請參閱＜  
 [交叉驗證 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)   
 [交叉驗證索引標籤 &#40;採礦精確度圖表檢視&#41;](../Topic/Cross-Validation%20Tab%20\(Mining%20Accuracy%20Chart%20View\).md)   
 [呼叫預存程序](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
  