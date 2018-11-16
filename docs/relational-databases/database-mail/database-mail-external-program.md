---
title: Database Mail 外部程式 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- external programs [Database Mail]
- DatabaseMail90.exe
- Database Mail [SQL Server], external programs
ms.assetid: bc124164-eb6e-4b7f-bf66-98a3113d02f7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 098cc286efc2d3672406e296bb78b5a0f494d4c9
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559285"
---
# <a name="database-mail-external-program"></a>Database Mail 外部程式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Database Mail 外部可執行檔是 **DatabaseMail.exe**，位於 **安裝的** MSSQL\Binn 目錄 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中。 有電子郵件訊息需要處理時，Database Mail 會使用「Service Broker 啟用」來啟動外部程式。 Database Mail 會啟動一個外部程式的執行個體。 外部程式則於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶的安全性內容中執行。  
  
 **本主題內容：**  
  
-   [Database Mail 外部程式概念](#ComponentsAndConcepts)  
  
-   [與設定 Database Mail 外部程式相關的工作](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> Database Mail 外部程式概念  
 外部程式啟動時，程式會使用「Windows 驗證」連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並開始處理電子郵件訊息。 若在指定的逾時期限內沒有訊息需要傳送，程式就會結束。 您可以使用「Database Mail 組態精靈」或 Database Mail 預存程序，來設定程式結束前需等待的時間長度。 如需詳細資訊，請參閱 [sysmail_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)服務帳戶的安全性內容中執行。  
  
 外部程式會將資訊儲存在 **msdb** 資料庫的系統資料表中。 若外部程式無法與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通訊，程式會將錯誤記錄到 Microsoft Windows 應用程式事件記錄檔中。 當您將 **[Database Mail 組態精靈]** 中 **[設定系統參數]** 對話方塊中的記錄層級設定為 **[詳細資訊]** 時，會提供額外的訊息記錄。  
  
 請注意，外部程式會為了提高效率而快取帳戶與設定檔資訊， 因此，對帳戶與設定檔的組態變更，可能要在幾分鐘後才會反映在外部程式中。  
  
##  <a name="RelatedTasks"></a> 與設定 Database Mail 外部程式相關的工作  
  
|組態工作|主題連結|  
|------------------------|----------------|  
|指定外部程式在結束之前的時間。|[sysmail_configure_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Database Mail 記錄與稽核](../../relational-databases/database-mail/database-mail-log-and-audits.md)   
 [Database Mail](../../relational-databases/database-mail/database-mail.md)  
  
  
