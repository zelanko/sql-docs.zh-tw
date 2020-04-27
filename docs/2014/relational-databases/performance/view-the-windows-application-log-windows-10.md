---
title: 檢視 Windows 應用程式記錄檔 (Windows 10) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- application logs [SQL Server]
- logs [SQL Server], application
- monitoring Windows NT application log [SQL Server]
- Windows NT application logs [SQL Server]
- displaying logs
- monitoring [SQL Server], events
- logs [SQL Server], viewing
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b18643f97a328dfee94bc5bfe125d6eddeae4efe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63150433"
---
# <a name="view-the-windows-application-log-windows"></a>檢視 Windows 應用程式記錄檔 (Windows)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為使用 Windows 應用程式記錄檔時，每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作階段都會將新事件寫入該記錄檔。 您每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時，並不會建立新的應用程式記錄檔，這和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]錯誤記錄檔不同。  
  
### <a name="to-view-the-windows-application-log"></a>若要檢視 Windows 應用程式記錄檔  
  
1.  在 **[開始]** 功能表上，指向 **[所有程式]**，再指向 **[系統管理工具]**，然後按一下 **[事件檢視器]**。  
  
2.  在 [事件檢視器] 中，按一下 **[應用程式]**。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件是以 [來源]  資料行的 **MSSQLSERVER** 項目識別 (具名執行個體則是以 _MSSQL$_ **<執行個體名稱>** 識別)。 SQL Server Agent 事件由 SQLSERVERAGENT 項目識別 (對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的具名執行個體，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 事件是由 **SQLAgent$** \<*執行個體名稱*> 加以識別)。 Microsoft Search 服務事件則以 **Microsoft Search**項目識別。  
  
4.  若要檢視不同電腦的記錄檔，請以滑鼠右鍵按一下 [事件檢視器]****，按一下 [連線到另一台電腦]****，然後完成 [選取電腦]**** 對話方塊。  
  
5.  (選擇性) 若只想顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件，請在 **[檢視]** 功能表中按一下 **[篩選]**，然後在 **[事件來源]** 清單中選擇 **[MSSQLSERVER]**。 若只想檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 事件，請改在 **[事件來源]** 清單中選取 **[SQLSERVERAGENT]** 。  
  
6.  若要檢視事件的詳細資訊，請按兩下該事件。  
  
## <a name="see-also"></a>另請參閱  
 [檢視 SQL Server 錯誤記錄檔 &#40;SQL Server Management Studio&#41;](../../ssms/sql-server-management-studio-ssms.md)  
  
  
