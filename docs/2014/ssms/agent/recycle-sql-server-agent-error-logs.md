---
title: 回收 SQL Server Agent 錯誤記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c0654dcc83e757751ac055192775c0ee958f26e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62753065"
---
# <a name="recycle-sql-server-agent-error-logs"></a>回收 SQL Server Agent 錯誤記錄檔
  使用此頁面回收 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤記錄檔。 回收記錄檔時會關閉目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤記錄檔，並在未重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務的情況下，啟動新的錯誤記錄檔。 請注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會保留九個最新的錯誤記錄檔。 如果已經有九個錯誤記錄檔存在，回收錯誤記錄檔會造成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 移除最舊的錯誤記錄檔。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 錯誤記錄檔](sql-server-agent-error-log.md)  
  
  
