---
title: MSSQLSERVER_9003 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d8d9266f4867918893af9f1298fbb3a82f8e8635
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver9003"></a>MSSQLSERVER_9003
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|9003|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LOG_INVALID_LSN|  
|訊息文字|傳遞到資料庫 '%.*ls' 記錄檔掃描的記錄檔掃描號碼 %S_LSN 無效。 這個錯誤可能表示資料損毀或記錄檔 (.ldf) 不符合資料檔案 (.mdf)。 如果是在複寫期間發生這個錯誤，請重新建立發行集。 否則，若該問題造成啟動失敗，則請從備份進行還原。|  
  
## <a name="explanation"></a>說明  
某個元件將無效的記錄序號傳遞給資料庫的記錄檔管理員。 這個問題的原因可能是複寫、損毀或主要資料檔案與記錄檔之間的不一致。  
  
## <a name="user-action"></a>使用者動作  
如果是在複寫期間發生這個錯誤，請重新建立發行集。 否則，請從備份進行還原。  
  
