---
title: MSSQL_ENG024070 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG024070 error
ms.assetid: 23ac7e00-fab6-429b-9f85-2736a322aa65
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 31421597871bfef0c02a15ce83bf486ea9cc6646
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048418"
---
# <a name="mssqleng024070"></a>MSSQL_ENG024070
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|24070|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|用戶端沒有必要的權限。|  
  
## <a name="explanation"></a>說明  
 這是不論是否使用複寫，都有可能引發的一般性錯誤。 如果是複寫拓撲中的伺服器，通常是因為使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 服務控制管理員 (而不是正確使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 組態管理員) 變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶，而引發錯誤。 當您在變更服務帳戶之後嘗試執行代理程式作業時，作業可能失敗，並會顯示訊息如下：  
  
 「 使用者的身分執行： \<UserAccount >。 複寫-複寫快照集子系統： 代理程式\<代理程式名稱 > 失敗。 以使用者身分執行： \<UserAccount >。 用戶端沒有必要的權限。 步驟失敗。 `[SQLSTATE 42000] (Error 14151)`. 步驟失敗。」  
  
 發生這個問題是因為 Windows 服務控制管理員無法授與權限給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的新服務帳戶。  
  
## <a name="user-action"></a>使用者動作  
 若要避免未來發生這個問題，一律要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員 (而非 Windows 服務控制管理員) 來變更服務帳戶及密碼。  
  
 若要解決這個問題，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，將服務帳戶變更回原始帳戶。 然後，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員變更為新帳戶。 當您執行此動作時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員會將新帳戶加入至下列安全性群組：  
  
 SQLServer2008SQLAgentUser$ComputerName$InstanceName  
  
 做為這個安全性群組的成員，便會授與新帳戶執行複寫代理程式作業所需的權限。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)   
 [管理複寫的登入與密碼](security/manage-logins-and-passwords-in-replication.md)   
 [SQL Server 組態管理員](../sql-server-configuration-manager.md)  
  
  
