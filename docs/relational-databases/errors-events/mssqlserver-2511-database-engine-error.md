---
title: MSSQLSERVER_2511 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c28be4ae43225cc4593291285c09115829be8da2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780442"
---
# <a name="mssqlserver_2511"></a>MSSQLSERVER_2511
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|2511|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_KEYS_OUT_OF_ORDER|  
|訊息文字|資料表錯誤：物件識別碼 %d，索引識別碼 %d，分割區識別碼 %I64d，配置單位識別碼 %I64d (類型 %.*ls)。 頁面 %S_PGID，位置 %d 和 %d 的索引鍵次序不對。|  
  
## <a name="explanation"></a>說明  
在指定的索引中偵測到次序不對的索引鍵。 包含索引鍵的頁面可能已損毀。  
  
## <a name="user-action"></a>使用者動作  
使用 ALTER INDEX REBUILD 陳述式來重建指定的索引。  
  
