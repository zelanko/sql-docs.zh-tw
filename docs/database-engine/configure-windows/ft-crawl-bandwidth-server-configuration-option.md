---
title: 全文檢索編目頻寬伺服器組態選項 | Microsoft Docs
description: 了解 [全文檢索耙梳頻寬] 選項。 了解此選項如何影響 SQL Server 在大型記憶體緩衝區集區中維護緩衝區的數量。
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
- large memory buffers
- memory [SQL Server], buffers
- ft crawl bandwidth option
ms.assetid: e5864ad9-92f5-43b5-95de-46d68ded8694
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 59caa1e868c4caab24afd17909c34f57c96f0005
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789787"
---
# <a name="ft-crawl-bandwidth-server-configuration-option"></a>全文檢索耙梳頻寬伺服器組態選項
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  使用 **ft crawl bandwidth** 選項，可指定大型記憶體緩衝區的集區可以成長到多大的大小。 大型記憶體緩衝區的大小是 4 MB。 **max** 參數值指定全文檢索記憶體管理員應該在大型緩衝集區中維持的最大緩衝區數目。 如果 **max** 值為零，則位在大型緩衝集區的緩衝區數目沒有上限。  
  
 **min** 參數指定必須在大型記憶體緩衝集區維持的最小記憶體緩衝區數目。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體管理員的要求下，所有額外緩衝集區都會釋放，但仍會維護最小數目的緩衝區。 但是，如果指定的 **min** 值是零，則會釋放所有記憶體緩衝區。  
  
 在某些情況下，目前配置的緩衝區數目小於 **min** 參數所指定的值。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [全文檢索通知頻寬伺服器組態選項](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
