---
title: MSSQLSERVER_9001 | Microsoft Docs
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
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1eaae857105a13a133c2fc9cd216d701df9f51d5
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver9001"></a>MSSQLSERVER_9001
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|9001|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LOG_NOT_AVAIL|  
|訊息文字|無法使用資料庫 '%.*ls' 的記錄檔。 相關錯誤訊息請查閱事件記錄檔。 解決任何錯誤，並重新啟動資料庫。|  
  
## <a name="explanation"></a>說明  
資料庫記錄檔已離線。 通常這種情況表示需要重新啟動資料庫的重大錯誤。  
  
## <a name="user-action"></a>使用者動作  
診斷其他錯誤並重新啟動 SQL Server 的執行個體 (如果它尚未自行重新啟動的話)。  
  

