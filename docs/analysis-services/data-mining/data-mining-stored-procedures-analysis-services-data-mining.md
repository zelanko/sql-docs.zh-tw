---
title: "資料採礦預存程序 (Analysis Services-資料採礦) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: stored procedures [Analysis Services], data mining
ms.assetid: a751856d-33bd-4788-9593-317b2826132d
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bf4b9b0fb2fe19d084c47d78d215f0001309af20
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="data-mining-stored-procedures-analysis-services---data-mining"></a>資料採礦預存程序 (Analysis Services - 資料採礦)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]從開始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]支援可以用任何 managed 語言撰寫的預存程序。 支援的 Managed 語言包括 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET、C# 和 Managed C++。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，您可以使用 **CALL** 陳述式直接呼叫預存程序，或是當作資料採礦延伸模組 (DMX) 查詢的一部分來呼叫。  
  
 如需呼叫 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 預存程序的詳細資訊，請參閱 [呼叫預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)。  
  
 如需可程式性的一般資訊，請參閱[資料採礦程式設計](../../analysis-services/data-mining-programming.md)。  
  
 如需如何撰寫資料採礦物件之程式的其他資訊，請參閱 MSDN Library 中的文件[SQL Server Data Mining Programmability](http://go.microsoft.com/fwlink/?LinkId=93735)(SQL Server 資料採礦可程式性)。  
  
> [!NOTE]  
>  當您查詢採礦模型，尤其是當您測試新的資料採礦方案時，您可能會發現呼叫由資料採礦引擎在內部使用的系統預存程序是很方便的事情。 您可以檢視這些系統預存程序的名稱，其方式是使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器上建立追蹤，然後建立、瀏覽及查詢資料採礦模型。 但是， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 不保證系統預存程序在不同版本之間的相容性，而且您絕對不能在實際系統中使用系統預存程序的呼叫。 為了提供相容性，您應該改用 DMX 或 XML/A 來建立自己的查詢。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [SystemGetCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterAccuracyResults &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
## <a name="see-also"></a>請參閱  
 [交叉驗證 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)   
 [交叉驗證索引標籤 &#40;採礦精確度圖表檢視 &#41;](http://msdn.microsoft.com/library/bd215a68-1ad7-4046-9c44-ec8e2be13a64)   
 [呼叫預存程序](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
  
