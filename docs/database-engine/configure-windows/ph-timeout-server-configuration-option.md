---
title: PH 逾時伺服器組態選項 | Microsoft Docs
description: 了解 [PH 逾時] 選項。 查看此選項如何限制全文檢索通訊協定處理常式配置來連線到 SQL Server 資料庫的時間。
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- time limit for protocol handler wait [SQL Server]
- timeout options [SQL Server], ph timeout option
- protocols [SQL Server], timing out
- ph timeout option
ms.assetid: ed19a07c-83fe-4582-9c9e-41b1ce571850
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a0173d6e5c5b10ac05b757f483518999fc526992
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730962"
---
# <a name="ph-timeout-server-configuration-option"></a>PH 逾時伺服器組態選項
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  使用 PH 逾時選項來指定全文檢索通訊協定處理常式在資料庫連接逾時之前，需先等候的時間 (以秒為單位)。預設值為 60 秒。 若連接嘗試因為暫時性的網路問題而逾時，請增加 ph timeout 值。  
  
 全文檢索通訊協定處理常式是由篩選背景程式主機所控管，而且可用來從 SQL Server 提取要編製全文檢索索引的資料。 如需有關全文檢索搜尋元件的詳細資訊，請參閱 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)。  
  
 嘗試提取資料列時，若通訊協定處理常式無法在指定的時間內連接到 SQL Server，則會報告該資料列逾時錯誤。 全文檢索收集程式會稍後會嘗試重新提取該資料列。 如需有關全文檢索收集程式的詳細資訊，請參閱 [擴展全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md)。  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
