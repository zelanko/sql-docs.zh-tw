---
title: 以單一使用者模式啟動 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- starting SQL Server, single-user mode
- single-user mode [SQL Server]
ms.assetid: 72eb4fc1-7af4-4ec6-9e02-11a69e02748e
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bd8666add4989876f3662bcd8b38a231a98c0b0c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="start-sql-server-in-single-user-mode"></a>以單一使用者模式啟動 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在某些情況下，您可能需要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] startup option -m **，在單一使用者模式下啟動**的執行個體。 例如，您可能想要變更伺服器組態選項，或復原損毀的 master 資料庫或其他系統資料庫。 這兩個動作都需要在單一使用者模式下啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 在單一使用者模式下啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可讓電腦本機管理員群組的任何成員以 sysadmin 固定伺服器角色的成員身分，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 如需詳細資訊，請參閱 [當系統管理員遭到鎖定時連接到 SQL Server](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)。  
  
 以單一使用者模式啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，請注意下列事項：  
  
-   只有一個使用者可以連接到伺服器。  
  
-   不會執行 CHECKPOINT 處理。 依預設，在啟動時會自動執行。  
  
> [!NOTE]  
>  連接到單一使用者模式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之前必須先停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務，否則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務會使用該連接，從而將其封鎖。  
  
以單一使用者模式啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 可以連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的物件總管可能會失敗，因為它需要一個以上的連接才能進行某些作業。 若要在單一使用者模式下管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，僅透過 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的查詢編輯器連接來執行 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，或使用 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)。  
  
當您搭配 **SQLCMD** 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 使用 **-m** 選項時，您可以限制指定用戶端應用程式的連線。 

> [!NOTE]
> 在 Linux 上，**SQLCMD** 必須大寫，如此處所示。

例如，**-m"SQLCMD"** 會限制連線為單一連線，且連線必須將自己識別為 **SQLCMD** 用戶端程式。 當您在單一使用者模式下啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而且有未知的用戶端應用程式佔用唯一可用的連接時，請使用這個選項。 若要透過 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的查詢編輯器進行連接，請使用 **-m"Microsoft SQL Server Management Studio - Query"**。  
  
> [!IMPORTANT]  
>  請勿將這個選項當做安全性功能使用。 用戶端應用程式會提供用戶端應用程式名稱，而且可能會在連接字串中提供假的名稱。  
  
## <a name="note-for-clustered-installations"></a>叢集安裝注意事項  
 如果是叢集環境中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在單一使用者模式下啟動時，叢集資源 dll 會用完可用的連接，藉此封鎖與伺服器的任何其他連接。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在此狀態下時，如果您嘗試將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 資源帶到線上，當 SQL 資源設定為可影響群組時，它可能會將此資源容錯移轉到另一個節點。  
  
 若要避開此問題，請使用下列程序：  
  
1.  從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 進階屬性中移除 –m 啟動參數。  
  
2.  讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源離線。  
  
3.  從這個群組的目前擁有者節點，從命令提示字元發出下列命令：  
    net start MSSQLSERVER /m  
  
4.  從叢集管理員或是容錯移轉叢集管理主控台確認 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源依然為離線狀態。  
  
5.  現在使用下列命令連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，並執行必要作業：SQLCMD -E -S\<伺服器名稱>。  
  
6.  當此操作完成之後，關閉命令提示字元，並透過叢集管理員將 SQL 和其他資源帶回線上。  
  
## <a name="see-also"></a>另請參閱  
 [啟動、停止或暫停 SQL Server Agent 服務](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)   
 [資料庫管理員的診斷連接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)   
 [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Database Engine 服務啟動選項](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
