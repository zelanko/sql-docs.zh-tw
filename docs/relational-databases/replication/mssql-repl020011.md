---
title: MSSQL_REPL020011 | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_REPL020011 error
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 445bc44fcd812f42965f843f8cb43d8c0e96c8fa
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="mssqlrepl020011"></a>MSSQL_REPL020011
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|20011|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|該處理無法執行 '%1' (在 '%2')。|  
  
## <a name="explanation"></a>說明  
 在許多情況下，異動複寫處理期間都會出現此錯誤，例如當記錄讀取器代理程式執行 **sp_replcmds** (處理序無法在 \<伺服器名稱> 上執行 'sp_replcmds') 或 **sp_repldone** (處理序無法在 \<伺服器名稱> 上執行 'sp_repldone' ) 時。  
  
## <a name="user-action"></a>使用者動作  
 如果在您剛從備份還原的資料庫中發生此錯誤，請務必按照備份與還原文件集中所述的步驟進行操作，包括執行 **sp_replrestart** (如有必要)。 如需相關資訊，請參閱 [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)。  
  
 此錯誤為內部處理錯誤，如果它在還原以外的情況下出現，通常表示必須移除並重新設定複寫。 如果您無法移除複寫，請連絡客戶支援部門尋求幫助。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)  
  
  
