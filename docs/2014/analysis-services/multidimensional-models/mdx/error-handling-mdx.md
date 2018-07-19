---
title: 錯誤處理 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
caps.latest.revision: 26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bbbe021cbb65803f79a4aa0a92791441e22e9cb6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37332678"
---
# <a name="error-handling-mdx"></a>錯誤處理 (MDX)
  每個 Cube 都可以控制多維度運算式 (MDX) 指令碼內錯誤的處理方式。 錯誤處理透過`ScriptErrorHandlingMode`列舉值。 此列舉值可能出現的值如下：  
  
 `IgnoreNone`  
 當 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 發現 MDX 指令碼中有任何錯誤時，可導致伺服器引發錯誤。  
  
 `IgnoreAll`  
 使伺服器忽略 MDX 指令碼中內含錯誤的所有命令，包括語法錯誤、名稱解析錯誤等等。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
