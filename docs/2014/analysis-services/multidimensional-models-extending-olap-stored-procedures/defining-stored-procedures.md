---
title: 定義預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- stored procedures [Analysis Services]
- OLAP [Analysis Services], stored procedures
- external routines [Analysis Services]
- stored procedures [Analysis Services], about stored procedures
ms.assetid: f9c57d91-f60f-4f0e-8f7f-d87f4ba97b7c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 69daca3a13cf5318e102002f0edfcb98b80ff9d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702763"
---
# <a name="defining-stored-procedures"></a>定義預存程序
  您可以使用預存程式從[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]呼叫外部常式。 您可以用任何 Common Language Runtime (CLR) 語言 (比如：C、C++、C#、Visual Basic，或 Visual Basic .NET)，來撰寫預存程序所呼叫的外部常式。 預存程序可以只建立一次，再從許多內容中呼叫，比如：其他預存程序、導出量值，或用戶端應用程式。 預存程序讓通用程式碼只需要開發一次並儲存在單一位置，可簡化 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的開發和實作。 預存程序可用來將 MDX 的原生功能未提供的商務功能，加入您的應用程式中。  
  
 本節提供了解、設計和實作預存程序所需的資訊。  
  
|主題|描述|  
|-----------|-----------------|  
|[設計預存程序](../multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|描述如何設計 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所使用的組件。|  
|[建立預存程序](creating-stored-procedures.md)|描述如何建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的組件。|  
|[呼叫預存程序](calling-stored-procedures.md)|提供有關如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中使用組件的資訊。|  
|[在預存程序中存取查詢內容](accessing-query-context-in-stored-procedures.md)|描述如何用組件來存取範圍及內容資訊。|  
|[設定預存程序的安全性](setting-security-for-stored-procedures.md)|描述如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中設定組件的安全性。|  
|[除錯預存程序](debugging-stored-procedures.md)|描述如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中偵錯組件。|  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型元件管理](../multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
