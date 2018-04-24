---
title: MSSQLSERVER_1401 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1401 (Database Engine error)
ms.assetid: 02928770-aa63-4509-8713-406c73e4cedc
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d30bfa0a55fcf15c5027f4fd7dcdceaf9c22d55
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver1401"></a>MSSQLSERVER_1401
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|1401|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBM_MASTERSTARTUP|  
|訊息文字|資料庫鏡像主執行緒常式啟動失敗，原因如下: %ls。 請更正錯誤的原因，然後重新啟動 SQL Server 服務。|  
  
## <a name="explanation"></a>說明  
鏡像控制執行緒啟動失敗。  
  
## <a name="user-action"></a>使用者動作  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄中，尋找在此訊息之前發生的相關錯誤。 請更正錯誤的原因，然後重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務 (MSSQLSERVER)。  
  
## <a name="see-also"></a>另請參閱  
[啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](~/database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
