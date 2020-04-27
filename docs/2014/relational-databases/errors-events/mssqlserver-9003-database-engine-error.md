---
title: MSSQLSERVER_9003 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c3d994f2166ae468a731203211eeb7a784118e65
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62912460"
---
# <a name="mssqlserver_9003"></a>MSSQLSERVER_9003
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|9003|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LOG_INVALID_LSN|  
|訊息文字|傳遞到資料庫 '%.*ls' 記錄檔掃描的記錄檔掃描號碼 %S_LSN 無效。 這個錯誤可能表示資料損毀或記錄檔 (.ldf) 不符合資料檔案 (.mdf)。 如果是在複寫期間發生這個錯誤，請重新建立發行集。 否則，若該問題造成啟動失敗，則請從備份進行還原。|  
  
## <a name="explanation"></a>說明  
 某個元件將無效的記錄序號傳遞給資料庫的記錄檔管理員。 這個問題的原因可能是複寫、損毀或主要資料檔案與記錄檔之間的不一致。  
  
## <a name="user-action"></a>使用者動作  
 如果是在複寫期間發生這個錯誤，請重新建立發行集。 否則，請從備份進行還原。  
  
  
