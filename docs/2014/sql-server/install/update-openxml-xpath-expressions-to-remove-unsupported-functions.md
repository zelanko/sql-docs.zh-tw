---
title: 更新 OPENXML XPath 運算式來移除不支援的函式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENXML queries
ms.assetid: b459abaf-8787-4b65-9231-ae30e5469fd0
caps.latest.revision: 17
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 87a35ea41c36250c1173df22204e6222dae0d384
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37172069"
---
# <a name="update-openxml-xpath-expressions-to-remove-unsupported-functions"></a>更新 OPENXML XPath 運算式來移除不受支援的函數
  Upgrade Advisor 偵測到使用了 XPath 功能。 升級之後，您可能會受到在 OPENXML 功能之 XPath 功能中所做變更的影響。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 MSXML 3.0 已經成為用來處理 OPENXML 查詢內使用之 XPath 運算式的基礎引擎。 MSXML 3.0 有較嚴格的 XPath 1.0 引擎，其中已移除下列函數的支援：  
  
-   format-number()  
  
-   formatNumber()  
  
-   current()  
  
-   element-available()  
  
-   function-available()  
  
-   system-property()  
  
## <a name="corrective-action"></a>更正動作  
 在 format-number() 和 formatNumber() 的情況中，您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 若為先前列出的其他不支援函數，沒有直接的因應措施。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
