---
title: PH 逾時伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- time limit for protocol handler wait [SQL Server]
- timeout options [SQL Server], ph timeout option
- protocols [SQL Server], timing out
- ph timeout option
ms.assetid: ed19a07c-83fe-4582-9c9e-41b1ce571850
caps.latest.revision: 28
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f0458fbfc8df8a2b662eb78131c43646f10618a4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171409"
---
# <a name="ph-timeout-server-configuration-option"></a>PH 逾時伺服器組態選項
  使用 PH 逾時選項來指定全文檢索通訊協定處理常式在資料庫連接逾時之前，需先等候的時間 (以秒為單位)。預設值為 60 秒。 若連接嘗試因為暫時性的網路問題而逾時，請增加 ph timeout 值。  
  
 全文檢索通訊協定處理常式是由篩選背景程式主機所控管，而且可用來從 SQL Server 提取要編製全文檢索索引的資料。 如需有關全文檢索搜尋元件的詳細資訊，請參閱 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)。  
  
 嘗試提取資料列時，若通訊協定處理常式無法在指定的時間內連接到 SQL Server，則會報告該資料列逾時錯誤。 全文檢索收集程式會稍後會嘗試重新提取該資料列。 如需有關全文檢索收集程式的詳細資訊，請參閱 [擴展全文檢索索引](../../relational-databases/indexes/indexes.md)。  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
