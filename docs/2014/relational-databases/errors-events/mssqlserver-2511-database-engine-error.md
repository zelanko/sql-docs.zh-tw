---
title: MSSQLSERVER_2511 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1748e8b483eecee43da921bd268d419408924af3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48062015"
---
# <a name="mssqlserver2511"></a>MSSQLSERVER_2511
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|2511|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_KEYS_OUT_OF_ORDER|  
|訊息文字|資料表錯誤: 物件識別碼 %d，索引識別碼 %d，分割區識別碼 %I64d，配置單位識別碼 %I64d (類型 %.*ls)。 頁面 %S_PGID，位置 %d 和 %d 的索引鍵次序不對。|  
  
## <a name="explanation"></a>說明  
 在指定的索引中偵測到次序不對的索引鍵。 包含索引鍵的頁面可能已損毀。  
  
## <a name="user-action"></a>使用者動作  
 使用 ALTER INDEX REBUILD 陳述式來重建指定的索引。  
  
  
