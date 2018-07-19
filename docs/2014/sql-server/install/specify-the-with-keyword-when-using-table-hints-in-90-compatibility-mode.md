---
title: 在 90 相容性模式中使用資料表提示時，請指定 WITH 關鍵字 |Microsoft Docs
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
- WITH keyword
- table hints [SQL Server]
ms.assetid: 7636cc85-5155-44db-baf6-df807761adb8
caps.latest.revision: 15
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fbf6b43149c0fbbd80a647696a327ef508904903
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37294028"
---
# <a name="specify-the-with-keyword-when-using-table-hints-in-90-compatibility-mode"></a>在 90 相容性模式中，使用資料表提示時，請指定 WITH 關鍵字
  唯有利用 WITH 關鍵字指定提示時，查詢的 FROM 子句中才支援資料表提示，但有些例外狀況。 如需詳細資訊，請參閱《[!INCLUDE[tsql](../../includes/tsql-md.md)] 線上叢書》中的＜FROM ([!INCLUDE[tsql](../../includes/tsql-md.md)])＞和＜資料表提示 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])＞主題。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 透過在資料表提示前加入 WITH 關鍵字，修改 FROM 子句中包含資料表提示的查詢。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
