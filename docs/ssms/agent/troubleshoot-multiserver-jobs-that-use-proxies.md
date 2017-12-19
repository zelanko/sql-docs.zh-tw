---
title: "針對使用 Proxy 的多伺服器作業進行疑難排解 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- proxies [SQL Server Agent], multiserver jobs
- jobs [SQL Server Agent], multiserver jobs using proxies
ms.assetid: fc579bd3-010c-4f72-8b5c-d0cc18a1f280
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b681674b1764282cf5cfc7ba4c75c70317fc093c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="troubleshoot-multiserver-jobs-that-use-proxies"></a>疑難排解使用 Proxy 的多伺服器作業
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 這是在目標伺服器上，於 Proxy 帳戶的環境下執行與 Proxy 建立關聯步驟的散發式作業。 如果使用 Proxy 帳戶從主要伺服器下載的作業步驟失敗，請在 **msdb** 資料庫的 **sysdownloadlist** 資料表中，檢查 **error_message** 資料行，以了解下列錯誤訊息：  
  
-   「此作業步驟需要 Proxy 帳戶，但目標伺服器已停用 Proxy 比對。」  
  
    若要解決此錯誤，請將 **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.***\<n*>**\SQLServerAgent\AllowDownloadedJobsToMatchProxyName** 登錄機碼設為 **1 (true)**。 依預設，這個子機碼設為 **0** (**False**)。 **MSSQL.**\<*n*> 的值是執行個體名稱，例如 **MSSQL.1** 或 **MSSQL.3**。  
  
-   「找不到 Proxy。」  
  
    若要解決此錯誤，請確定目標伺服器上有 Proxy 帳戶，且帳戶名稱與執行該作業步驟的主要伺服器 Proxy 帳戶相同。  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry_md.md)]  
  
## <a name="see-also"></a>另請參閱  
[建立多伺服器環境](../../ssms/agent/create-a-multiserver-environment.md)  
  
