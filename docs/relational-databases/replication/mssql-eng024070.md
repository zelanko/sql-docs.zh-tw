---
title: MSSQL_ENG024070 | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG024070 error
ms.assetid: 23ac7e00-fab6-429b-9f85-2736a322aa65
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 205b2f0da8ad8a8f3523b8d554c84235df45d619
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="mssqleng024070"></a>MSSQL_ENG024070
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|24070|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|用戶端沒有必要的權限。|  
  
## <a name="explanation"></a>說明  
 這是不論是否使用複寫，都有可能引發的一般性錯誤。 如果是複寫拓撲中的伺服器，通常是因為使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 服務控制管理員 (而不是正確使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 組態管理員) 變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶，而引發錯誤。 當您在變更服務帳戶之後嘗試執行代理程式作業時，作業可能失敗，並會顯示訊息如下：  
  
 `Executed as user: \<UserAccount>. Replication-Replication Snapshot Subsystem: agent \<AgentName> failed. Executed as user: \<UserAccount>. A required privilege is not held by the client. The step failed. [SQLSTATE 42000] (Error 14151). The step failed.`  
  
 發生這個問題是因為 Windows 服務控制管理員無法授與權限給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的新服務帳戶。  
  
## <a name="user-action"></a>使用者動作  
 若要避免未來發生這個問題，一律要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員 (而非 Windows 服務控制管理員) 來變更服務帳戶及密碼。  
  
 若要解決這個問題，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，將服務帳戶變更回原始帳戶。 然後，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員變更為新帳戶。 當您執行此動作時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員會將新帳戶加入至下列安全性群組：  
  
 SQLServer2008SQLAgentUser$ComputerName$InstanceName  
  
 做為這個安全性群組的成員，便會授與新帳戶執行複寫代理程式作業所需的權限。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [管理複寫的登入與密碼](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)  
  
  

