---
title: "定義預存程序 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- stored procedures [Analysis Services]
- OLAP [Analysis Services], stored procedures
- external routines [Analysis Services]
- stored procedures [Analysis Services], about stored procedures
ms.assetid: f9c57d91-f60f-4f0e-8f7f-d87f4ba97b7c
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b70d20ea8ad3cc108076261b692129bf72ccb6ef
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="defining-stored-procedures"></a>定義預存程序
  您可以使用預存程序來呼叫外部常式從[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 您可以用任何 Common Language Runtime (CLR) 語言 (比如：C、C++、C#、Visual Basic，或 Visual Basic .NET)，來撰寫預存程序所呼叫的外部常式。 預存程序可以只建立一次，再從許多內容中呼叫，比如：其他預存程序、導出量值，或用戶端應用程式。 預存程序讓通用程式碼只需要開發一次並儲存在單一位置，可簡化 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的開發和實作。 預存程序可用來將 MDX 的原生功能未提供的商務功能，加入您的應用程式中。  
  
 本節提供了解、設計和實作預存程序所需的資訊。  
  
|主題|Description|  
|-----------|-----------------|  
|[設計預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|描述如何設計 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所使用的組件。|  
|[建立預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md)|描述如何建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的組件。|  
|[呼叫預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)|提供有關如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中使用組件的資訊。|  
|[存取預存程序的查詢內容](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/accessing-query-context-in-stored-procedures.md)|描述如何用組件來存取範圍及內容資訊。|  
|[正在設定預存程序安全性](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)|描述如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中設定組件的安全性。|  
|[偵錯預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)|描述如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中偵錯組件。|  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型組件管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
