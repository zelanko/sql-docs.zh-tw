---
title: "回收 SQL Server Agent 錯誤記錄檔 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3404d3eceb9a57f9807ed2b47515fddb7331646a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="recycle-sql-server-agent-error-logs"></a>回收 SQL Server Agent 錯誤記錄檔
使用此頁面回收 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 錯誤記錄檔。 回收記錄檔時會關閉目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 錯誤記錄檔，並在未重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務的情況下，啟動新的錯誤記錄檔。 請注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會保留九個最新的錯誤記錄檔。 如果已經有九個錯誤記錄檔存在，回收錯誤記錄檔會造成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 移除最舊的錯誤記錄檔。  
  
## <a name="see-also"></a>另請參閱  
[SQL Server Agent 錯誤記錄檔](../../ssms/agent/sql-server-agent-error-log.md)  
  
