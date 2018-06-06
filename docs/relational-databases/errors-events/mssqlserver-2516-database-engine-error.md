---
title: MSSQLSERVER_2516 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c42dd135eace8e81b2423e2e70e4c09eb6baf1b0
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver2516"></a>MSSQLSERVER_2516
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|2516|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_REPAIR_DIFF_MAP_INVALIDATED|  
|訊息文字|修復導致資料庫 NAME 的差異式點陣圖無效。 差異備份鏈已中斷。 您必須執行完整的資料庫備份，然後才能執行差異備份。|  
  
## <a name="explanation"></a>說明  
在修復錯誤 MSSQLEngine_2515 時，會傳回這項參考用訊息。  
  
## <a name="user-action"></a>使用者動作  
執行完整的資料庫備份。  
  
## <a name="see-also"></a>另請參閱  
[建立完整資料庫備份 &#40;SQL Server&#41;](~/relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
