---
title: MSSQLSERVER_926 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 926 (Database Engine error)
ms.assetid: 57e01668-883b-4be4-84a8-a111caaf0486
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4afdc9adae6f968ca89ff1a9b2bf9e5b67992037
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62912470"
---
# <a name="mssqlserver_926"></a>MSSQLSERVER_926
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|926|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DB_SUSPECT|  
|訊息文字|資料庫 '%.*ls' 無法開啟。 它已經由復原標示成 SUSPECT。 如需詳細資訊，請參閱 SQL Server 錯誤記錄檔。|  
  
## <a name="explanation"></a>說明  
 資料庫標示為有疑問，因為復原程序未能將資料庫回復為一致交易狀態。 這可能發生在下列作業：  
  
-   啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
-   附加資料庫。  
  
-   使用 RESTORE 資料庫或 RESTORE LOG 程序。  
  
## <a name="user-action"></a>使用者動作  
 查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，了解錯誤的原因。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 因復原失敗而重新啟動，請查看先前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，了解復原失敗的原因。  
  
 如果復原程序是因為持續發生 I/O 錯誤、損毀頁或其他可能的硬體問題，請先解決根本的硬體問題，再使用備份還原資料庫。 如果沒有備份可供使用，請考慮使用 DBCC CHECKDB 的修復選項。  
  
 如果無法解決這個問題，請連絡您的主要支援提供者。 請準備好 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔以供檢閱。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 資料庫的備份與還原](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [sysdatabases &#40;Transact-sql&#41;](/sql/relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql)   
 [資料庫卸離與附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
