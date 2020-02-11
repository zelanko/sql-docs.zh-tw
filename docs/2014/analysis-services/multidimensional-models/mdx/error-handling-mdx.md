---
title: 錯誤處理（MDX） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 611e7636f9a5cd6393da4a8412b6c02bcc9ddaf8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074681"
---
# <a name="error-handling-mdx"></a>錯誤處理 (MDX)
  每個 Cube 都可以控制多維度運算式 (MDX) 指令碼內錯誤的處理方式。 透過 `ScriptErrorHandlingMode` 列舉值便可完成錯誤處理。 此列舉值可能出現的值如下：  
  
 `IgnoreNone`  
 當發現 MDX 腳本中有任何錯誤[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]時，會導致伺服器引發錯誤。  
  
 `IgnoreAll`  
 使伺服器忽略 MDX 指令碼中內含錯誤的所有命令，包括語法錯誤、名稱解析錯誤等等。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
