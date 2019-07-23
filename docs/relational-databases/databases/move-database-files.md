---
title: 移動資料庫檔案 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: c53e9ee51714ebfcce81a722f78a4f79cbc2530f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067322"
---
# <a name="move-database-files"></a>移動資料庫檔案
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，您可以在 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 陳述式的 FILENAME 子句中指定新的檔案位置，以移動系統和使用者資料庫。 可以使用此方式來移動資料、記錄以及全文檢索目錄檔案。 在下列狀況下這個方法將非常有用：  
  
-   失敗復原。 例如，資料庫因硬體失敗而導致在質疑模式下或被關閉。  
  
-   計畫的重新放置。  
  
-   排程的磁碟維護重新放置。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[移動使用者資料庫](../../relational-databases/databases/move-user-databases.md)|描述將使用者資料庫檔案和全文檢索目錄檔案移到新位置的程序。|  
|[移動系統資料庫](../../relational-databases/databases/move-system-databases.md)|描述將系統資料庫檔案移到新位置的程序。|  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [資料庫卸離與附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
