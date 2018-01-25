---
title: "全文檢索編目最大範圍伺服器組態選項 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- crawls [full-text search]
- max full-text crawl range option
ms.assetid: a49de86b-0891-4dcd-89c0-ead30aab00e0
caps.latest.revision: "24"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6b88107838d3507dfdaa888a462f29fc880b8be3
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="max-full-text-crawl-range-server-configuration-option"></a>全文檢索搜耙最大範圍伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 **max full-text crawl range** 選項可最佳化 CPU 使用率，這會在完整搜耙期間增進搜耙效能。 使用這個選項，您可以指定完整索引搜耙期間 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 應該使用的資料分割數目。 例如，如果有多個 CPU 且其使用率不是最好的，則您可以增加這個選項的最大值。 除了這個選項之外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 還會使用一些其他因素，如資料表中的資料列數目及 CPU 數目，來判斷實際使用的資料分割數目。  
  
 此選項的預設值為 4、最小值為 1，而最大值為 256。 變更此選項僅會影響後續的搜耙。 這個選項設定中的變更將不會影響進行中的搜耙。  
  
 **max full-text crawl range** 選項是進階選項。 如果您要使用 **sp_configure** 系統預存程序來變更設定，只有當 **show advanced options** 設為 1 時，才能變更 **max full-text crawl range** 。 設定會立即生效，伺服器不必重新啟動。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
