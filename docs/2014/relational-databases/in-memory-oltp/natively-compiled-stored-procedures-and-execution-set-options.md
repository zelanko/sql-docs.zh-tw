---
title: 原生編譯的預存程序和執行 Set 選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c1869cf7-9030-4d18-85d6-0e419a4e9af7
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 87ac7e07c0153f2221c3d5eda402b070711ffca3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035430"
---
# <a name="natively-compiled-stored-procedures-and-execution-set-options"></a>原生編譯的預存程序和執行 Set 選項
  工作階段選項在不可部分完成的區塊內是固定的。 預存程序的執行不會受到工作階段的 SET 選項所影響。 不過，某些 SET 選項 (例如 SET NOEXEC 和 SET SHOWPLAN_XML) 會造成預存程序 (包括原生編譯的預存程序) 不執行。  
  
 已開啟任何 STATISTICS 選項執行原生編譯的預存程序時，統計資料是針對整個程序蒐集而非每個陳述式。 如需詳細資訊，請參閱 [SET STATISTICS IO &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-io-transact-sql)、[SET STATISTICS PROFILE &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-profile-transact-sql)、[SET STATISTICS TIME &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-time-transact-sql) 和 [SET STATISTICS XML &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-xml-transact-sql)。 若要在原生編譯預存程序中，取得每個陳述式層級上的執行統計資料，請在 sp_statement_completed 事件上使用擴充事件工作階段，當預存程序執行中的所有個別查詢完成時，就會開始此事件。 如需建立擴充事件工作階段的詳細資訊，請參閱 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)。  
  
 `SHOWPLAN_XML` 支援原生編譯的預存程序。 原生編譯的預存程序不支援 `SHOWPLAN_ALL` 和 `SHOWPLAN_TEXT`。  
  
 原生編譯的預存程序不支援 `SET FMTONLY`。 請改用 [sp_describe_first_result_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程序](natively-compiled-stored-procedures.md)  
  
  
