---
title: "指定事件轉送伺服器 | Microsoft Docs"
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
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3a888bf925f0deec6b774891d13da7548d1fe28f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="designate-an-events-forwarding-server-sql-server-management-studio"></a>指定事件轉送伺服器 (SQL Server Management Studio)
此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中指定 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 將事件轉送到哪一部伺服器。 請注意，事件轉送適用於在伺服器之間轉送的事件，而不適用於在單一電腦上裝載之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 執行個體之間轉送的事件。 同時請注意，若要接收轉送的事件，則警示管理伺服器必須是預設的 SQL Server 執行個體。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [Security](#Security)  
  
-   **若要使用下列項目指定事件轉送伺服器：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-designate-an-events-forwarding-server"></a>指定事件轉送伺服器  
  
1.  在 **[物件總管]** 中，按一下加號展開伺服器，從此伺服器轉送事件到另一部伺服器。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]，然後選取 [屬性]。  
  
3.  在 [SQL Server Agent 屬性 - <伺服器名稱>] 對話方塊的 [選取頁面] 底下，選取 [進階]。  
  
4.  在 **[SQL Server 事件轉送]**下，選取 **[轉送事件到另一部伺服器]** 核取方塊。  
  
5.  在 **[伺服器]** 清單中選取伺服器，然後在 **[事件]**下選取下列其中一項：  
  
    -   選取 **[未處理的事件]** ，只轉送本機警示尚未處理的事件。  
  
    -   選取 **[所有事件]** ，轉送所有的事件，不論本機警示是否已處理。  
  
6.  在 **[如果事件的嚴重性等於或高於]** 清單中，按一下會開始將事件轉送至選定伺服器的嚴重性層級。  
  
7.  完成後，請按一下 **[確定]**。  
  

