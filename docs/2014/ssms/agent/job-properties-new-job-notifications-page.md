---
title: 作業屬性：新增作業 （通知頁面） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10cee6f0d5bf62178c71d25b8eb5682c22bbbe3b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52797683"
---
# <a name="job-properties-new-job-notifications-page"></a>作業屬性：新增作業 （通知頁面）
  使用此頁面來設定當作業完成時，[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 要執行的動作。  
  
## <a name="options"></a>選項。  
 **電子郵件**  
 選取此選項，即可在作業完成時傳送電子郵件。 選取此選項之後，選擇要通知的操作員及觸發通知的條件：**當作業成功時**;**當作業失敗時**; 或**作業完成時**。  
  
 **頁面**  
 選取此選項，即可在作業完成時將電子郵件傳送給操作員的呼叫器。 選取此選項之後，指定要通知的操作員及觸發通知的條件：**當作業成功時**;**當作業失敗時**; 或**作業完成時**。  
  
 **Net Send**  
 選取此選項，即可在作業完成時使用 Net Send 來通知操作員。 選取此選項之後，指定要通知的操作員及觸發通知的條件：**當作業成功時**;**當作業失敗時**; 或**作業完成時**。  
  
 **寫入 Windwos 應用程式事件記錄**  
 選取此選項，即可在作業完成時將項目寫入應用程式事件記錄檔。 選取此選項之後，指定要寫入之項目的條件：**當作業成功時**;**當作業失敗時**; 或**作業完成時**。  
  
 **自動刪除作業**  
 選取此選項，即可在作業完成時刪除作業。 選取此選項之後，指定觸發刪除作業的條件：**當作業成功時**;**當作業失敗時**; 或**作業完成時**。  
  
## <a name="see-also"></a>另請參閱  
 [實作作業](implement-jobs.md)   
 [設定 SQL Server Agent Mail 使用 Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
  
