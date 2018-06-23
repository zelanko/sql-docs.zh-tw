---
title: MSSQLSERVER_9001 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 9001 (Database Engine error)
ms.assetid: a54de936-90c6-4845-aa96-29d32f154601
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c1b57637cee601cde328bc079ab907629591b5f3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035715"
---
# <a name="mssqlserver9001"></a>MSSQLSERVER_9001
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|9001|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LOG_NOT_AVAIL|  
|訊息文字|無法使用資料庫 '%.*ls' 的記錄檔。 相關錯誤訊息請查閱事件記錄檔。 解決任何錯誤，並重新啟動資料庫。|  
  
## <a name="explanation"></a>說明  
 資料庫記錄檔已離線。 通常這種情況表示需要重新啟動資料庫的重大錯誤。  
  
## <a name="user-action"></a>使用者動作  
 診斷其他錯誤並重新啟動 SQL Server 的執行個體 (如果它尚未自行重新啟動的話)。  
  
  