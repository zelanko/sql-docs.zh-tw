---
title: "偵錯商務邏輯處理常式 (複寫程式設計) | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- merge replication business logic handlers [SQL Server replication]
- business logic handlers [SQL Server replication]
- BusinessLogicModule class
ms.assetid: edd0d17a-0e9c-4c28-8395-a7d47e8ce3d6
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 83358d1d13961f3b2a4ffc9bdf7ce1d2f594ae6a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="debug-a-business-logic-handler-replication-programming"></a>偵錯商務邏輯處理常式 (複寫程式設計)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 使用商務邏輯處理常式，以便在同步處理合併訂閱期間叫用自訂商務邏輯。 如需詳細資訊，請參閱[在合併同步處理期間執行商務邏輯](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)。  
  
 合併式複寫重新調整器 (replrec.dll) 會呼叫包含此商務邏輯的 Managed 程式碼組件。 在大部分情況下，會在合併代理程式執行所在的電腦上執行 replrec.dll 和自訂商務邏輯 (如果是提取訂閱，會在訂閱者上；如果是發送訂閱，則會在散發者上)。 如果是 Web 同步處理的情況或 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者的情況，會在 Web 伺服器上執行此調整器和自訂商務邏輯。  
  
### <a name="to-debug-a-business-logic-handler-on-a-local-computer"></a>在本機電腦上偵錯商務邏輯處理常式  
  
1.  設定發行和散發、建立發行集，以及建立發行集的訂閱。 如需詳細資訊，請參閱[設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)和[建立、修改及刪除發行集和發行項 &#40;複寫&#41;](../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md)。  
  
2.  建立及註冊商務邏輯處理常式。 如需相關資訊，請參閱 [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)。  
  
3.  在以程式設計方式同步啟動合併代理程式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 中，建立 Replication Management Objects (RMO) 專案。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
4.  在商務邏輯處理常式程式碼中設定中斷點 (在所偵錯的方法中或是類別建構函式中)。 如需有關可以在商務邏輯處理常式中實作之方法的詳細資訊，請參閱 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 方法主題。  
  
5.  在偵錯模式下建立此商務邏輯處理常式，並在步驟 1 註冊的位置中部署此組件和偵錯符號檔 (.pdb)。  
  
    > [!NOTE]  
    >  若要簡化偵錯，請建立一個同時包含商務邏輯處理常式專案和同步處理訂閱之專案的 Visual Studio .NET 方案。 在此情況下，請將同步處理專案設定為啟始專案，並設定建立環境，將商務邏輯組件部署到步驟 1 偵錯時所註冊的位置中。  
  
6.  針對訂閱或發行集資料庫執行插入、更新或刪除命令。 此命令和執行位置取決於所偵錯的方法而定。  
  
7.  在偵錯模式下從步驟 3 啟動此專案，以同步處理訂閱。  
  
8.  假設未設定任何其他中斷點，而且複寫了適當的命令，則當到達商務邏輯處理常式中的中斷點時，會停止執行。  
  
### <a name="to-debug-a-business-logic-handler-on-a-web-server-using-web-synchronization-or-for-a-sql-server-compact-subscriber"></a>使用 Web 同步處理在 Web 伺服器上偵錯商務邏輯處理常式，或是針對 SQL Server Compact 訂閱者進行偵錯  
  
1.  設定發行和散發、建立發行集，以及建立發行集的提取訂閱。 此發行集必須支援 Web 同步處理或 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者。  
  
2.  建立及註冊商務邏輯處理常式。 如需相關資訊，請參閱 [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)。  
  
3.  在商務邏輯處理常式程式碼中設定中斷點 (在所偵錯的方法中或是類別建構函式中)。 如需有關可以在商務邏輯處理常式中實作之方法的詳細資訊，請參閱 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 方法主題。  
  
4.  在偵錯模式下建立此商務邏輯處理常式，並在步驟 1 註冊的位置中，於 Web 伺服器上部署此組件和偵錯符號檔 (.pdb)。  
  
    > [!NOTE]  
    >  如果因為此組件在使用中而導致無法建立商務邏輯處理常式，請在此 Web 伺服器的命令提示字元上輸入 `iisreset` 命令，以重設 Web 伺服器。  
  
5.  在啟用 Web 同步處理的情況下同步處理訂閱。 在同步處理期間，Web 伺服器會載入註冊的組件。  
  
6.  使用 Visual Studio .NET 偵錯工具，附加到 Web 伺服器上的下列其中一個處理序：  
  
    -   w3wp.exe - Windows Server 2003。  
  
    -   inetinfo.exe - Windows 2000 和 Windows XP。  
  
7.  在 **[輸出]** 視窗中，檢查偵錯輸出，以確認註冊之組件的符號已正確載入。 如果未載入符號，請確定步驟 4 中是否複製了正確的 .pdb 檔案，並重複步驟 5。  
  
8.  針對訂閱或發行集資料庫執行插入、更新或刪除命令。 此命令和執行位置取決於所偵錯的方法而定。  
  
9. 使用 Visual Studio 偵錯工具，附加到 w3wp.exe 處理序。  
  
10. 使用 Web 同步處理再次同步處理訂閱。  
  
11. 假設未設定任何其他中斷點，而且複寫了適當的命令，則當到達商務邏輯處理常式中的中斷點時，會停止執行。  
  
## <a name="see-also"></a>另請參閱  
 [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
