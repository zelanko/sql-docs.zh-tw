---
title: 設定目標伺服器的輪詢間隔 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- interval for polling [SQL Server]
- target servers [SQL Server], polling interval
- polling interval [SQL Server]
ms.assetid: 4ffbbefa-77fb-442e-a77c-cb8c6cab9f3c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1578bbefc9ae17baae56799d943e5ae6186628ea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63033621"
---
# <a name="set-the-polling-interval-for-target-servers"></a>Set the Polling Interval for Target Servers
  本主題描述如何設定[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 從主伺服器重新整理資訊到目標伺服器的頻率。 作業是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 執行的一系列指定動作。 多重伺服器作業是一個主要伺服器執行於一或多個目標伺服器上的作業。  
  
-   **開始之前：** [安全性](#Security)  
  
-   **若要設定目標伺服器的輪詢間隔，請使用：**  [SQL Server Management Studio](#SSMS)、 [transact-sql](#TSQL)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 每一個目標伺服器可以同時執行相同作業的一個執行個體。 每個目標伺服器會定期輪詢主要伺服器、下載任何指派到目標伺服器的新作業之副本，然後中斷連接。 目標伺服器會先在本機執行作業，然後再重新連接到主要伺服器，以便上傳作業結果的狀態。  
  
> [!NOTE]  
>  如果當目標伺服器嘗試上傳作業狀態時無法存取主要伺服器，作業狀態會被多工緩衝處理，直到可以存取主要伺服器為止。  
  
###  <a name="Security"></a> Security  
 如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](implement-sql-server-agent-security.md) ＞和＜ [Choose the Right SQL Server Agent Service Account for Multiserver Environments](choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)＞。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
 **設定目標伺服器的輪詢間隔**  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  在 [SQL Server Agent]****，再指向 [多伺服器管理]****，然後按一下 [管理目標伺服器]****。  
  
3.  在 **[目標伺服器狀態]** 索引標籤上，按一下 **[公佈指示]**。  
  
4.  在 **[指示類型]** 清單中選取 **[設定輪詢間隔]**。  
  
5.  在 **[輪詢間隔]** 方塊中，輸入介於 10 到 28,800 之間的秒數，這是目標伺服器輪詢主要伺服器之前所需經過的時間。  
  
6.  在 **[收件者]** 下，執行下列其中一項：  
  
    1.  如果所有的目標伺服器共用相同的輪詢間隔，請按一下 **[所有目標伺服器]** 。  
  
    2.  如果並非所有的目標伺服器都共用相同的輪詢間隔，請按一下 **[下列目標伺服器]** ，然後選取將使用此輪詢間隔的每一部目標伺服器。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
 **設定目標伺服器的輪詢間隔**  
  
1.  在 [物件總管] 中，連接到 Database Engine 的執行個體，然後展開該執行個體。  
  
2.  在工具列上，按一下 [新增查詢]****。  
  
3.  在查詢視窗中，使用[sp_post_msx_operation &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql)系統預存程式來設定目標伺服器的輪詢間隔。  
  
## <a name="see-also"></a>另請參閱  
 [sysdownloadlist &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysdownloadlist-transact-sql)  
  
  
