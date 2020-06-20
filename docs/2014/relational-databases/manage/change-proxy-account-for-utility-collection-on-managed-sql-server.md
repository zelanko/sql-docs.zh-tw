---
title: 在 SQL Server （SQL Server 公用程式）的受控執行個體上變更公用程式收集組的 Proxy 帳戶 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ff37ba8b-a08c-4109-b6e2-5748c995a52c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c1f78c711b19b742176517962a45618f112a67cc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85023804"
---
# <a name="change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server-sql-server-utility"></a>變更 SQL Server 受管理的執行個體上之公用程式收集組的 Proxy 帳戶 (SQL Server 公用程式)
  此主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中變更 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]受管理的執行個體上公用程式收集組的 Proxy 帳戶。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-change-the-proxy-account-for-the-utility-collection-set-on-a-managed-instance-of-sql-server"></a>若要變更 SQL Server 受管理的執行個體上之公用程式收集組的 Proxy 帳戶  
  
1.  從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的受管理的執行個體。  
  
    -   在 SSMS 內的 [公用程式總管]  中，按一下 [受管理的執行個體]  節點。  
  
    -   在 [公用程式總管]  清單檢視中，以滑鼠右鍵按一下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱，然後選取 [移除受控執行個體...]  。如需詳細資訊，請參閱 [從 SQL Server 公用程式中移除 SQL Server 執行個體](remove-an-instance-of-sql-server-from-the-sql-server-utility.md)。  
  
2.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內再次註冊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
    -   在 SSMS 的 [公用程式總管]  中，以滑鼠右鍵按一下 [受控執行個體]  節點，然後選取 [新增受控執行個體...]  。  
  
    -   依照提示完成精靈，指定新的 Proxy 帳戶。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)   
 [疑難排解 SQL Server 公用程式](../../database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
