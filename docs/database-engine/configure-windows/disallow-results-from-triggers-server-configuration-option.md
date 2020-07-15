---
title: 不允許來自觸發程序的結果伺服器組態選項 | Microsoft Docs
description: 了解 [不允許來自觸發程序的結果] 選項。 了解此選項如何避免未針對使用結果集進行設計的應用程式發生問題。
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], result sets
- result sets [SQL Server], triggers
- disallow results from triggers option
ms.assetid: 47149073-307d-47a5-b7d2-66a737d3231d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8cbe799b72a88da9785e778cb0688fe3ff1a3f44
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772531"
---
# <a name="disallow-results-from-triggers-server-configuration-option"></a>不允許來自觸發程序的結果伺服器組態選項
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  使用 **disallow results from triggers** 選項來控制觸發程序是否要傳回結果集。 傳回結果集的觸發程序可能會導致非專用的應用程式發生非預期的行為。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 建議您將此值設定為 1。  
  
 若設為 1， **disallow results from triggers** 選項就會設為 ON。 這個選項的預設值是 0 (OFF)。 若此選項設為 1 (ON)，則觸發程序嘗試傳回結果集的任何動作都會失敗，而使用者會收到下列錯誤訊息：  
  
 「訊息 524，層級 16，狀態 1，程序 \<Procedure Name>，行 \<Line#>」  
  
 「觸發程序傳回一個結果集，而且伺服器選項 'disallow_results_from_triggers' 為 True。」  
  
 [不允許來自觸發程序的結果] 選項是套用於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體層級，且它會決定執行個體中所有現有觸發程序的行為。  
  
 **disallow results from triggers** 選項是進階選項。 若使用 **sp_configure** 系統預存程序來變更設定，只有當 [顯示進階選項] 設為 1 時，才能變更觸發程序不允許的結果。 設定會立即生效，伺服器不必重新啟動。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
