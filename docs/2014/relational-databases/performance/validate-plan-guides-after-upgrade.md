---
title: 升級之後驗證計畫指南 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], validating after upgrade
ms.assetid: a55ebd88-6f58-454d-b1c4-991b88add522
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c3f3f8fd278d1141417adec4f1ef6a1faced386c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48145058"
---
# <a name="validate-plan-guides-after-upgrade"></a>升級之後驗證計畫指南
  建議您將應用程式升級為新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，重新評估和測試計畫指南定義。 效能微調需求和計畫指南符合的行為有可能會變更。 雖然無效的計畫指南不會導致查詢失敗，但是系統將不會使用此計畫指南來編譯計畫，而且此計畫可能不是最佳選擇。 將資料庫升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之後，我們建議您執行下列工作：  
  
-   使用 [sys.fn_validate_plan_guide](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql) 函數來驗證現有的計畫指南。  
  
-   使用擴充事件，透過 [Plan Guide Unsuccessful](../event-classes/plan-guide-unsuccessful-event-class.md) 事件，在一段時間內監視是否有誤導的計畫。  
  
  
