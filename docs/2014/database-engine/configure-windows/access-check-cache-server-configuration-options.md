---
title: access check cache 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
- access check cache bucket count
- access check cache quota
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: feed895eeb7b11b4c41c51c4c26859a1057d2733
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86158756"
---
# <a name="access-check-cache-server-configuration-options"></a>存取檢查快取伺服器組態選項
當資料庫物件是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所存取時，存取檢查會在稱為 **access check result cache**的內部結構中進行快取。 
  
**存取檢查快取 bucket 計數**選項可控制用於存取檢查結果快取的雜湊值區數目。 

[**存取檢查**快取配額] 選項會控制儲存在存取檢查結果快取中的專案數。 達到最大專案數時，會從存取檢查結果快取中移除最舊的專案。
  
預設值 0 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在管理這些選項。 從 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ，預設值會轉譯為下列內部設定：
-   針對存取檢查快取 bucket 計數，值0會設定 x86 架構的預設值為256，而 x64 和 IA-64 架構則為 2048 bucket。
-   針對存取檢查快取配額，值0會為 x86 架構設定1024專案的預設值，以及 x64 和 IA-64 架構的 28192048 bucket。

在罕見的情況下，可以變更這些選項來提升效能。 例如，如果使用太多記憶體，您可能會想要減少存取檢查結果快取的大小。 或者，如果在重新計算許可權時遇到高 CPU 使用量，您可能會想要增加存取檢查結果快取的大小。

> [!IMPORTANT]
> Microsoft 建議只要變更 Microsoft 客戶支援服務所導向的那些選項。
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
