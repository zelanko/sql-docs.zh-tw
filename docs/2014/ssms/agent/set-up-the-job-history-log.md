---
title: 設定作業記錄 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 018e5c49-d3a0-4504-851a-f70996a34bb7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 613c0ccae7be912bd3bec63905b838b7f07b59b0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63033573"
---
# <a name="set-up-the-job-history-log"></a>Set Up the Job History Log
  本主題描述如何設定[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業歷程記錄。  
  
-   **開始之前**  [安全性](#Security)  
  
-   **若要使用下列項目設定作業記錄：**  [SQL Server Management Studio](#SSMS)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
 **若要設定作業記錄**  
  
1.  在 [物件總管]**** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]****，然後按一下 [屬性]****。  
  
3.  在 **[SQL Server Agent 屬性]** 對話方塊中，選取 **[記錄]** 頁面。  
  
4.  從下列選項中選擇：  
  
    1.  核取 **[限制作業記錄大小]**，然後輸入作業記錄的最大資料列數，以及每一個作業的最大資料列數。  
  
    2.  核取 **[自動移除代理程式記錄]**，並指定時間週期，比此週期要舊的記錄將會從記錄清除。  
  
## <a name="see-also"></a>另請參閱  
 [執行作業](implement-jobs.md)   
 [監視作業活動](monitor-job-activity.md)   
 [建立作業](create-jobs.md)  
  
  
