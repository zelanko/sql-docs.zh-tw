---
title: Affinity64 I/O Mask 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- binding processors [SQL Server]
- affinity64 I/O mask option
ms.assetid: d304eae7-5116-40ee-a0fa-0a3c0bc20c01
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7449be34c7697f770b18357c465da41cd57164b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210158"
---
# <a name="affinity64-input-output-mask-server-configuration-option"></a>affinity64 輸入輸出伺服器組態選項
  **affinity64 I/O mask** 會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁碟 I/O 繫結至指定的 CPU 子集 (與 **affinity I/O mask** 選項很相似)。 請使用 **affinity I/O mask** 來繫結前 32 個處理器，然後使用 **affinity64 I/O mask** 來繫結電腦上剩餘的處理器。 如果您重新設定 **affinity64 I/O mask**，就必須重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 這個選項只出現在 64 位元版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [affinity Input-Output mask 伺服器組態選項](affinity-input-output-mask-server-configuration-option.md)   
 [監視資源使用量 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
