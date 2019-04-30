---
title: 即使當觸發程序的巢狀結構是 OFF 時，才引發巢狀 AFTER 觸發程序 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- DML triggers, nested
- nested triggers option
- triggers [SQL Server], nested
ms.assetid: 94d72960-676e-40d9-81bc-08bffe778110
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8b9e66e04cc6e4ae179816b6f0b679178c2e7052
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267594"
---
# <a name="nested-after-trigger-fires-even-when-trigger-nesting-is-off"></a>即使觸發程序巢狀結構是 OFF，也會引發巢狀 AFTER 觸發程序
  Upgrade Advisor 偵測到在一個或多個資料表上所定義的 INSTEAD OF 觸發程序內，有巢狀的 AFTER 觸發程序。 即使 `nested triggers` 伺服器組態選項設定為 0，巢狀 AFTER 觸發程序仍可能引發。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 即使 `nested triggers` 伺服器組態選項設為 0，INSTEAD OF 觸發程序內部的第一個巢狀 AFTER 觸發程序仍會引發。 不過，在此設定下，後續的 AFTER 觸發程序不會引發。  
  
## <a name="corrective-action"></a>更正動作  
 請檢閱應用程式中是否有巢狀觸發程序，以判斷當 `nested triggers` 伺服器組態選項設定為 0 時，這些應用程式的新行為是否仍符合您的商務規則，然後進行適當的修改。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
