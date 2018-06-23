---
title: 升級之後驗證計畫指南 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-plan-guides
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- plan guides [SQL Server], validating after upgrade
ms.assetid: a55ebd88-6f58-454d-b1c4-991b88add522
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 01d0fb2a81694dcdf2acb9202db61780a6b7104e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131477"
---
# <a name="validate-plan-guides-after-upgrade"></a>升級之後驗證計畫指南
  建議您將應用程式升級為新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，重新評估和測試計畫指南定義。 效能微調需求和計畫指南符合的行為有可能會變更。 雖然無效的計畫指南不會導致查詢失敗，但是系統將不會使用此計畫指南來編譯計畫，而且此計畫可能不是最佳選擇。 將資料庫升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之後，我們建議您執行下列工作：  
  
-   使用 [sys.fn_validate_plan_guide](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql) 函數來驗證現有的計畫指南。  
  
-   使用擴充事件，透過 [Plan Guide Unsuccessful](../event-classes/plan-guide-unsuccessful-event-class.md) 事件，在一段時間內監視是否有誤導的計畫。  
  
  
