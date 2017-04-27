---
title: "設定警示呼叫器號碼的格式 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pager addresses [SQL Server]
- SQL Server Agent, alerts
- formats [SQL Server], pager addresses
- pager notifications [SQL Server]
- addresses [SQL Server]
- alerts [SQL Server], pager addresses
ms.assetid: a9797d01-1050-442c-9038-ed4bfee1e76a
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f202f1e48ca7c9ef030b5434514c4c5d6a93300b
ms.lasthandoff: 04/11/2017

---
# <a name="format-pager-addresses-for-alerts"></a>Format Pager Addresses for Alerts
此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 [!INCLUDE[tsql](../../includes/tsql_md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中格式化 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 警示的呼叫器號碼。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [Security](#Security)  
  
-   **若要使用下列項目，格式化呼叫器號碼：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
依預設， **系統管理員 (sysadmin)** 固定伺服器角色的成員可以檢視警示的相關資訊。 其他使用者必須被授與 **msdb** 資料庫的 **SQLAgentOperatorRole** 固定資料庫角色。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-format-pager-addresses"></a>若要格式化呼叫器號碼  
  
1.  在 **[物件總管]**中，按一下加號展開伺服器，此伺服器包含要傳送至呼叫器的警示。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]，然後選取 [屬性]。  
  
3.  在 **[選取頁面]**底下，選取 **[警示系統]**。  
  
4.  在 [呼叫器電子郵件位址格式] 欄位的 [收件者] 和 [副本] 方塊中，輸入呼叫器號碼的前置詞和後置詞。 當傳送通知時，就會插入操作員的實際呼叫器號碼。  
  
5.  在 **[主旨]** 方塊中，輸入主旨行前置詞或後置詞。  
  
6.  選取 [將電子郵件的內文包含在通知訊息中] 核取方塊，表示會在呼叫器訊息中加入完整的電子郵件訊息 (而不是僅有主旨行)。  
  
7.  完成後，請按一下 **[確定]**。  
  

