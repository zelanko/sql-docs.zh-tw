---
title: 原生編譯的預存程序和執行 Set 選項 | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c1869cf7-9030-4d18-85d6-0e419a4e9af7
caps.latest.revision: 5
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 908b7e49c2af671773645f010435b2cc97c90afc
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="natively-compiled-stored-procedures-and-execution-set-options"></a>原生編譯的預存程序和執行 Set 選項
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

工作階段選項在不可部分完成的區塊內是固定的，如[不可部分完成的區塊](atomic-blocks-in-native-procedures.md)中所述。 由於需要不可部分完成的區塊，因此預存程序的執行不會受到工作階段的 SET 選項所影響。 不過，某些 SET 選項 (例如 SET NOEXEC 和 SET SHOWPLAN_XML) 會造成預存程序 (包括原生編譯的預存程序) 不執行。   
  
 已開啟任何 STATISTICS 選項執行原生編譯的預存程序時，統計資料是針對整個程序蒐集而非每個陳述式。 如需詳細資訊，請參閱 [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)、[SET STATISTICS PROFILE &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-profile-transact-sql.md)、[SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md) 和 [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md)。 若要在原生編譯預存程序中，取得每個陳述式層級上的執行統計資料，請在 sp_statement_completed 事件上使用擴充事件工作階段，當預存程序執行中的所有個別查詢完成時，就會開始此事件。 如需建立擴充事件工作階段的詳細資訊，請參閱 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)。  
  
 原生編譯的預存程序支援 **SHOWPLAN_XML**。 原生編譯的預存程序不支援**SHOWPLAN_ALL** 和 **SHOWPLAN_TEXT** 。  
  
 原生編譯的預存程序不支援**SET FMTONLY** 。 請改用 [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
