---
description: MSSQL_REPL020011
title: MSSQL_REPL020011 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL020011 error
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 3bf143f39b38decc7a51a7eb71385b0cf4684360
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97432213"
---
# <a name="mssql_repl020011"></a>MSSQL_REPL020011
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>訊息詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|20011|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|該處理無法執行 '%1' (在 '%2')。|  
  
## <a name="explanation"></a>說明  
 在許多情況下，異動複寫處理期間都會出現此錯誤，例如當記錄讀取器代理程式執行 **sp_replcmds** (處理序無法在 \<ServerName> 上執行 'sp_replcmds') 或 **sp_repldone** (處理序無法在 \<ServerName> 上執行 'sp_repldone' ) 時。  
  
## <a name="user-action"></a>使用者動作  
 如果在您剛從備份還原的資料庫中發生此錯誤，請務必按照備份與還原文件集中所述的步驟進行操作，包括執行 **sp_replrestart** (如有必要)。 如需詳細資訊，請參閱 [備份與還原快照式和異動複寫的策略](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)。  
  
 此錯誤為內部處理錯誤，如果它在還原以外的情況下出現，通常表示必須移除並重新設定複寫。 如果您無法移除複寫，請連絡客戶支援部門尋求幫助。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)  
  
  
