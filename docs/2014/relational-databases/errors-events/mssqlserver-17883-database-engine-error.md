---
title: MSSQLSERVER_17883 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17883 (Database Engine error)
ms.assetid: adaf1c04-e397-4a69-90b8-9353a37277ea
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2f9f712ed8d37872c90eff773e81a657fb96c296
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62915267"
---
# <a name="mssqlserver_17883"></a>MSSQLSERVER_17883
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|17883|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SRV_SCHEDULER_NONYIELDING|  
|訊息文字|處理序 %ld:%ld:%ld (0x%lx) 工作者 0x%p 在排程器 %ld 上似乎沒有產量。 執行緒建立時間: %I64d. 已使用的約略執行緒 CPU：核心 %I64d ms，使用者 %I64d ms。 處理序使用情形 %d%%。 系統閒置率 %d%%。 間隔: %I64d 毫秒。|  
  
## <a name="explanation"></a>說明  
 表示執行緒在排程器上沒有任何產量可能有問題。  這個問題可能是由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的錯誤或者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 沒有取得足夠的循環可執行所造成。  如果執行緒最後有產量，這個錯誤就可能會消失。  
  
## <a name="user-action"></a>使用者動作  
 如果系統負載過大，請減少負載，否則請連絡 Microsoft 客戶支援服務。  
  
  
