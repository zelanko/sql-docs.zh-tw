---
title: 防止自動啟動 SQL Server 的實例（SQL Server 組態管理員） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, stopping
- SQL Server, automatic startup
- canceling automatic startup
- stopping SQL Server
- preventing automatic startups [SQL Server]
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8f93f5abc749f589ab4208b3a4c9434ca63b8769
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935032"
---
# <a name="prevent-automatic-startup-of-an-instance-of-sql-server-sql-server-configuration-manager"></a>避免自動啟動 SQL Server 的執行個體 (SQL Server 組態管理員)
  此主題描述如何使用 SQL Server 組態管理員，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中防止 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體自動啟動。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通常會設定為自動啟動。 不過您也可以將該執行個體的啟動模式改設為手動。  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-prevent-automatic-startup-of-an-instance-of-sql-server"></a>避免自動啟動 SQL Server 的執行個體  
  
1.  指向 **[開始]** 功能表上的 **[所有程式]** ，然後依序指向 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]** ，再按一下 **[SQL Server 組態管理員]** 。  
  
2.  在 SQL Server 組態管理員中，展開 [**服務**]，然後按一下 [ **SQL Server**]。  
  
3.  在 [詳細資料] 窗格中，以滑鼠右鍵按一下 [MSSQLServer]****，然後按一下 [屬性]****。  
  
4.  在 [ **SQL Server \<**_instancename_**> 屬性**] 對話方塊的 [**屬性**] 方塊中，將 [**啟動模式]** 的值設定為 [**手動**]。  
  
5.  按一下 **[確定]** 關閉 [ **SQL Server \<**_instancename_**> 屬性**] 對話方塊，然後關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager。  
  
## <a name="see-also"></a>另請參閱  
 [啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](start-stop-pause-resume-restart-sql-server-services.md)  
  
  
