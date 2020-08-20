---
description: MSSQLSERVER_844
title: MSSQLSERVER_844 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 844 (Database Engine error)
ms.assetid: 2060c886-1226-4066-bc0c-de90a1cfb82b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e6b92d297b2e948baadf30947ba51cee48822120
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499454"
---
# <a name="mssqlserver_844"></a>MSSQLSERVER_844
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|844|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|BUFLATCH_TIMEOUT_CONTINUE|  
|訊息文字|等候緩衝閂時發生逾時 -- 類型 %d，bp %p，頁面 %d:%d，狀態 %#x，資料庫識別碼: %d，配置單位識別碼: %I64d%ls，工作 0x%p : %d，等候時間 %d，旗標 0x%I64x，主控工作 0x%p。  繼續等候。|  
  
## <a name="explanation"></a>說明  
處理序正在等候取得閂鎖。 造成這個問題的原因可能是由於 I/O 作業花費太多時間才完成。 這種錯誤通常是其他工作封鎖了系統處理序所造成的結果。 在某些情況下，這項錯誤可能是硬體故障的結果。  
  
## <a name="user-action"></a>使用者動作  
請嘗試下列方法，以避免發生這項錯誤：  
  
-   減少工作負載。  
  
-   查看錯誤記錄檔或事件記錄檔中相關聯的 I/O 失敗。 I/O 失敗通常表示磁碟功能有問題。  
  
-   查看錯誤記錄檔，找出沒有產量的工作和其他重大錯誤。  
  
-   如果經常發生諸如判斷提示之類的重大錯誤，請解決這些問題。  
  
如果持續發生錯誤，請連絡 Microsoft 客戶服務及支援中心。  
  
