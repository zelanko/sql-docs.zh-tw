---
title: MSSQLSERVER_1458 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1458 (Database Engine error)
ms.assetid: adc78c59-a6f2-432b-9a07-fdd1dc2b9026
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f4764d1299488f5f6089f6a029f7e44a9dd712a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62859722"
---
# <a name="mssqlserver1458"></a>MSSQLSERVER_1458
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1458|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBM_FAILREDO_ON_PRIMARY|  
|訊息文字|'%.*ls' 資料庫的主體副本發現錯誤 %d，狀態 %d，嚴重性 %d。 資料庫鏡像已暫停。 請嘗試解決錯誤狀況，然後繼續執行鏡像。|  
  
## <a name="explanation"></a>說明  
這個訊息表示主體資料庫遭遇錯誤，導致資料庫鏡像暫停。  
  
## <a name="user-action"></a>使用者動作  
在大部分情況下，這個錯誤都會自動修正。 如果問題持續發生，重新啟動資料庫或伺服器執行個體通常就能修正問題。 如需詳細資訊，請查看每個夥伴的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔，以取得在此訊息之前發生的相關錯誤。  
  
## <a name="see-also"></a>另請參閱  
[監視資料庫鏡像 &#40;SQL Server&#41;](~/database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
