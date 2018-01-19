---
title: SHUTDOWN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHUTDOWN_TSQL
- SHUTDOWN
dev_langs: TSQL
helpviewer_keywords:
- SQL Server, stopping
- shutting down SQL Server
- SHUTDOWN statement
- stopping SQL Server
- immediately stopping SQL Server
ms.assetid: c8b03ff9-688c-4fe8-86e8-bd6bd401c9a4
caps.latest.revision: "31"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e4cf8ea2b61d4f1acb69ea489a5116a701264469
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="shutdown-transact-sql"></a>SHUTDOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  立即停止 SQL Server。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SHUTDOWN [ WITH NOWAIT ]   
```  
  
## <a name="arguments"></a>引數  
 WITH NOWAIT  
 選擇性。 在不執行每個資料庫之檢查點的情況下，關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在嘗試終止所有使用者處理序之後，結束 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 當重新啟動伺服器時，會執行未完成的交易之回復作業。  
  
## <a name="remarks"></a>備註  
 除非使用 WITHNOWAIT 選項，否則 SHUTDOWN 會向下[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的：  
  
1.  停用登入 (的成員除外**sysadmin**和**serveradmin**固定伺服器角色)。  
  
    > [!NOTE]  
    >  若要顯示所有目前的使用者清單，請執行**sp_who**。  
  
2.  等待目前在執行中的 Transact-SQL 陳述式或預存程序完成。 顯示所有作用中的處理序和鎖定的清單，請執行**sp_who**和**sp_lock**分別。  
  
3.  在每個資料庫中插入檢查點。  
  
 使用 SHUTDOWN 陳述式盡量縮短自動復原工作所需的時間成員**sysadmin**固定伺服器角色重新啟動[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 您也可以利用其他工具和方法來停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 所有這些工具和方法都會在所有資料庫中發出一個檢查點。 您可以從資料快取記憶體中清除已認可的資料，再停止伺服器：  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
-   藉由執行**net stop mssqlserver**從命令提示字元的預設執行個體，或執行 **net stop mssql$ * * * instancename*從命令提示字元的具名執行個體。  
  
-   使用 [控制台] 中的 [服務]。  
  
 如果**sqlservr.exe**已啟動的命令提示字元中，按 CTRL + C 會關閉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 不過，按 CTRL+C 不會插入檢查點。  
  
> [!NOTE]  
>  使用這些方法的任一種來停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，會將 `SERVICE_CONTROL_STOP` 訊息傳給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="permissions"></a>Permissions  
 SHUTDOWN 權限指派給成員**sysadmin**和**serveradmin**固定的伺服器角色，而且它們不能轉讓。  
  
## <a name="see-also"></a>另請參閱  
 [檢查點 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sqlservr 應用程式](../../tools/sqlservr-application.md)   
 [啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
