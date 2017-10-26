---
title: MSSQLSERVER_3417 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3417 (Database Engine error)
ms.assetid: 005829c8-cf57-4828-818a-bbe8ee2e00f0
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a24a6c95f5ccd79fe4eb3af627be689755469a56
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3417"></a>MSSQLSERVER_3417
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|3417|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|REC_BADMASTER|  
|訊息文字|無法復原 master 資料庫。 SQL Server 無法執行。 Restore master from a full backup, repair it, or rebuild it. 如需有關如何重建 master 資料庫的詳細資訊，請參閱《SQL Server 線上叢書》。|  
  
## <a name="explanation"></a>說明  
SQL Server 無法啟動 **master** 資料庫。 如果無法讓 **master** 或 **tempdb** 上線，SQL Server 就無法執行。 這項錯誤通常在其他錯誤之前發生。 請查閱錯誤記錄檔，找出根本的原因。  
  
## <a name="user-action"></a>使用者動作  
還原資料庫備份或修復資料庫。  
  

