---
title: "建立 SQL Server 資料庫警示 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database performance [SQL Server], alerts
- alerts [SQL Server], creating
- thresholds [SQL Server]
- database alerts [SQL Server]
- tuning databases [SQL Server], alerts
- monitoring performance [SQL Server], alerts
- monitoring server performance [SQL Server], alerts
- database monitoring [SQL Server], alerts
- server performance [SQL Server], alerts
ms.assetid: 0511136a-1b6b-4095-aa45-39e77b67aba2
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 67aaf5ab44e5584fc50851dd797ad7cbc62f3ffc
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-sql-server-database-alert"></a>建立 SQL Server 資料庫警示
  您可以使用「系統監視器」來建立警示，讓它在達到「系統監視器」計數器的臨界值時引發。 為了回應此警示，「系統監視器」可啟動某個應用程式，諸如撰寫來處理此警示條件的自訂應用程式。 例如，您可以建立一個警示，讓它在死結 (Deadlock) 個數超過特定數值時引發。  
  
 您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來定義警示。 如需詳細資訊，請參閱 [警示](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef)。  
  
 如需使用「系統監視器」來建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫警示的詳細資訊，請參閱[設定 SQL Server 資料庫警示 &#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  
