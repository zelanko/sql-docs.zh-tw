---
title: 在80相容性模式中，會忽略索引視圖定義中的資料表提示，而且在90模式或更新版本中不允許使用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- query hints [SQL Server]
- indexed views [SQL Server], query hints
ms.assetid: 405dfcff-a3a6-4e6d-a53a-ed77bbacdd13
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69a6bae06b1cb5d7a727ff2582f10bccf1e21ca8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66091811"
---
# <a name="table-hints-in-indexed-view-definitions-are-ignored-in-80-compatibility-mode-and-are-not-allowed-in-90-mode-or-later"></a>在 80 相容性模式中，將忽略索引檢視定義中的資料表提示，而在 90 或之後的模式中則不允許
  在 90 或之後的相容性模式中，不允許在索引檢視的定義中使用資料表提示。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的下列主題：＜設計索引檢視＞、＜建立索引檢視＞和＜查詢提示 ([!INCLUDE[tsql](../../includes/tsql-md.md)])＞。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 您必須將資料表提示從索引檢視的定義中移除。 不論使用的相容性模式為何，我們都建議您測試應用程式。 透過測試應用程式，您可以確保在建立、更新和存取索引檢視時 (包括索引檢視與查詢相符時)，應用程式會如預期方式執行。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
