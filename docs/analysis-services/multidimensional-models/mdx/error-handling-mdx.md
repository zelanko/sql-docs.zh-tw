---
title: 錯誤處理 (MDX) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e7575a598342dfabd66bc15a8f67b3b8ca70f690
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="error-handling-mdx"></a>錯誤處理 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  每個 Cube 都可以控制多維度運算式 (MDX) 指令碼內錯誤的處理方式。 透過 **ScriptErrorHandlingMode** 列舉值便可完成錯誤處理。 此列舉值可能出現的值如下：  
  
 **IgnoreNone**  
 當 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 發現 MDX 指令碼中有任何錯誤時，可導致伺服器引發錯誤。  
  
 **IgnoreAll**  
 使伺服器忽略 MDX 指令碼中內含錯誤的所有命令，包括語法錯誤、名稱解析錯誤等等。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
