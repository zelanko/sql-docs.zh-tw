---
title: "移動資料庫檔案 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- files [SQL Server], moving
- data files [SQL Server], moving
- file moving [SQL Server]
- moving full-text catalogs
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- scheduled disk maintenance [SQL Server]
- moving files
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
caps.latest.revision: "34"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 50a05ea742b9a049dc69b8683be8026603ac00f2
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="move-database-files"></a>移動資料庫檔案
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，您可以在 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 陳述式的 FILENAME 子句中指定新的檔案位置，以移動系統和使用者資料庫。 可以使用此方式來移動資料、記錄以及全文檢索目錄檔案。 在下列狀況下這個方法將非常有用：  
  
-   失敗復原。 例如，資料庫因硬體失敗而導致在質疑模式下或被關閉。  
  
-   計畫的重新放置。  
  
-   排程的磁碟維護重新放置。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[移動使用者資料庫](../../relational-databases/databases/move-user-databases.md)|描述將使用者資料庫檔案和全文檢索目錄檔案移到新位置的程序。|  
|[移動系統資料庫](../../relational-databases/databases/move-system-databases.md)|描述將系統資料庫檔案移到新位置的程序。|  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [資料庫卸離和附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
