---
title: 定義預存程序 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6a251da65ced87835b6de50d71bd60658db17fd9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="defining-stored-procedures"></a>定義預存程序
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  您可以使用預存程序來呼叫外部常式從[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 您可以用任何 Common Language Runtime (CLR) 語言 (比如：C、C++、C#、Visual Basic，或 Visual Basic .NET)，來撰寫預存程序所呼叫的外部常式。 預存程序可以只建立一次，再從許多內容中呼叫，比如：其他預存程序、導出量值，或用戶端應用程式。 預存程序讓通用程式碼只需要開發一次並儲存在單一位置，可簡化 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的開發和實作。 預存程序可用來將 MDX 的原生功能未提供的商務功能，加入您的應用程式中。  
  
 本節提供了解、設計和實作預存程序所需的資訊。  
  
|主題|Description|  
|-----------|-----------------|  
|[設計預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|描述如何設計 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所使用的組件。|  
|[建立預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md)|描述如何建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的組件。|  
|[呼叫預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)|提供有關如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中使用組件的資訊。|  
|[在預存程序中存取查詢內容](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/accessing-query-context-in-stored-procedures.md)|描述如何用組件來存取範圍及內容資訊。|  
|[設定預存程序的安全性](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)|描述如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中設定組件的安全性。|  
|[偵錯預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)|描述如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中偵錯組件。|  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型組件管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
