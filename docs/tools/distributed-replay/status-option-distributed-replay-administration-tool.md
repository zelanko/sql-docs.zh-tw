---
title: "狀態選項 （Distributed 的 Replay 管理工具） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea89386e-1598-4412-8b37-680d14b2a5b6
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6831b370359b7540621eb8d69bdf070689edd9a2
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="status-option-distributed-replay-administration-tool"></a>狀態選項 (Distributed Replay 管理工具)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理工具 **DReplay.exe**是命令列工具，可用以與 Distributed Replay Controller 通訊。 此主題描述 **status** 命令列選項與對應的語法。  
  
 **status** 選項會查詢控制器，並顯示目前的狀態。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示")更多系統管理工具語法所使用之語法慣例的詳細資訊，請參閱[TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>語法  
  
```  
  
dreplay status [-m controller] [-f status_interval]  
```  
  
#### <a name="parameters"></a>參數  
 **-m** *controller*  
 指定控制器的電腦名稱。 您可以使用 "`localhost`" 或 "`.`" 表示本機電腦。  
  
 如果未指定 **-m** 參數，則會使用本機電腦。  
  
 **-f** *status_interval*  
 指定顯示狀態的頻率 (以秒計)。  
  
 如果未指定 **-f** 參數，預設間隔為 30 秒。  
  
## <a name="examples"></a>範例  
 在下列範例中，每隔 60 秒顯示目前狀態。 `localhost` 值指出控制器服務與管理工具在同一部電腦上執行。  
  
```  
dreplay status –m localhost -f 60  
```  
  
## <a name="permissions"></a>Permissions  
 您必須以互動使用者、本機使用者或網域使用者帳戶來執行管理工具。 若要使用本機使用者帳戶，管理工具和控制器必須在同一部電腦上執行。  
  
 如需詳細資訊，請參閱 [Distributed Replay 安全性](../../tools/distributed-replay/distributed-replay-security.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Distributed 的 Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Transact-SQL 偵錯工具](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  
