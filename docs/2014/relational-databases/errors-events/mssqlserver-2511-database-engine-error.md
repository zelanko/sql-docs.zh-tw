---
title: MSSQLSERVER_2511 | Microsoft Docs
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
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 9cfc320d29448dfa829e8741643d79df5c80061f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131500"
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
  
  