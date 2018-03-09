---
title: "設計預存程序 |Microsoft 文件"
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- stored procedures [Analysis Services], designing
- dependent assemblies [Analysis Services]
- assemblies [Analysis Services]
ms.assetid: af4e7bd5-041b-4a40-9942-0ef6a3af46c6
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4b8b145a22f7d309fbaf69c1da3f6f4bb068fad5
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="designing-stored-procedures"></a>設計預存程序
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
管理的物件模型分析管理物件 (AMO) 和用戶端導向的物件模型 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX® Data Objects (多維度) (ADO MD)，二者都可在預存程序中使用。  
  
 預存程序必須在被呼叫的多維度運算式 (MDX) 層級可以看見的範圍內 (伺服器或資料庫)。 不過，一旦叫用預存程序後，其範圍就不限於其父系下的動作。 預存程序可以在伺服器上的任何位置進行變更或修改，只受限於叫用它之使用者處理序的安全性限制，或是它正在執行之交易的限制。  
  
 伺服器範圍的程序可以在伺服器的所有內容中使用。 資料庫範圍的預存程序，只有在定義它們之資料庫的資料庫內容中才看得見。  
  
 如同所有的 MDX 函數，必須先解析預存程序才能繼續 MDX 工作階段；在執行時，預存程序會鎖定 MDX 工作階段。 除非有特定原因需暫止 MDX 工作階段，等候使用者互動，否則不建議使用者互動 (例如對話方塊)。  
  
## <a name="dependent-assemblies"></a>相依組件  
 所有相依組件都必須載入 Common Language Runtime (CLR) 所要尋找的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體中。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將相依組件儲存在與主組件相同的資料夾中，所以 CLR 會自動解析組件中函數的所有函數參考。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型組件管理](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定義預存程序](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
