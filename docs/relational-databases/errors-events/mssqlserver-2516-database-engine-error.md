---
title: MSSQLSERVER_2516 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70ad1489ad5644d40e29d4f37aacabdd2bb88a8e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver2516"></a>MSSQLSERVER_2516
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
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
  
