---
title: access check cache 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- access check cache option
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
caps.latest.revision: 8
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ba3df614d843c6a1c5a4fb12bc7c8b17cc9784da
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135660"
---
# <a name="access-check-cache-server-configuration-options"></a>存取檢查快取伺服器組態選項
  當資料庫物件是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所存取時，存取檢查會在稱為 **access check result cache**的內部結構中進行快取。 **access check cache quota** 和 **access check cache bucket count** 選項會控制用於 **access check result cache**的項目數和雜湊值區數。 在罕見的情況下，可以變更這些選項來提升效能。  
  
 預設值 0 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在管理這些選項。 Microsoft 建議只要變更 Microsoft 客戶支援服務所導向的那些選項。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
