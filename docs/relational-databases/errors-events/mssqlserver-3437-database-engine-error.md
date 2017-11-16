---
title: MSSQLSERVER_3437 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3437 (Database Engine error)
ms.assetid: b38216e2-b650-43bd-97af-061d54f60031
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 62fcf4360a9b5eefc971bf0f5443a9e9e96004aa
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3437"></a>MSSQLSERVER_3437
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|3437|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|NODTC|  
|訊息文字|復原資料庫 '%.*ls' 時發生錯誤。 無法連接 Microsoft 分散式交易協調器 (MS DTC)，檢查交易 %S_XID 的完成狀態。 請修正 MS DTC，再次執行復原。|  
  
## <a name="explanation"></a>說明  
資料庫關閉時，使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 的一個或多個分散式交易未完成。 此資料庫的復原失敗，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法連接 MS DTC 以完成或回復交易。  
  
## <a name="user-action"></a>使用者動作  
若要復原此資料庫，您必須先解決 MS DTC 的問題。 若要調查 MS DTC 的問題，請檢查 Windows 事件記錄檔。 如果無法解決 MS DTC 問題並復原資料庫，請還原資料庫備份。  
  

