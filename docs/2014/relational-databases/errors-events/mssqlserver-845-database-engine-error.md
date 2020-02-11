---
title: MSSQLSERVER_845 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 845 (Database Engine error)
ms.assetid: 8fff6ad4-234c-44be-b123-e25d5e1cd63e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9d98be02727582d4f9201ec7f47c3cdb8db5a56b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761921"
---
# <a name="mssqlserver_845"></a>MSSQLSERVER_845
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|845|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|BUFLATCH_TIMEOUT|  
|訊息文字|等候緩衝閂類型 %d (資料庫識別碼 %d，頁面 %S_PGID) 時發生逾時。|  
  
## <a name="explanation"></a>說明  
 處理序一直等候要取得閂鎖，但該處理序等候到時間限制過期卻仍無法取得。 如果 I/O 作業完成需要花費太長時間 (通常是因為其他工作封鎖了系統處理序)，可能就會發生這種情形。 在某些情況下，這項錯誤可能是硬體故障的結果。  
  
## <a name="user-action"></a>使用者動作  
 執行下列事項或可避免此錯誤發生：  
  
-   降低工作負載。  
  
-   確認錯誤記錄檔或事件記錄檔中是否有相關聯的 I/O 失敗。 I/O 失敗通常是因磁碟異常所造成。  
  
-   查看錯誤記錄檔，找出沒有產量的工作和其他重大錯誤。  
  
-   如果經常發生諸如判斷提示之類的重大錯誤，請解決這些問題。  
  
 如果持續發生錯誤，請連絡 Microsoft 客戶服務及支援中心。  
  
  
