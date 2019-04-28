---
title: 取得 DDL 觸發程序的資訊 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- metadata [SQL Server], triggers
- status information [SQL Server], DDL triggers
- DDL triggers, metadata
ms.assetid: 462becea-292a-4b9e-bb98-533e89733911
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8d5e59264036380f6c8b5c9e73df5a6700c4b1ef
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62698210"
---
# <a name="get-information-about-ddl-triggers"></a>取得 DDL 觸發程序的詳細資訊
  本章節所列的目錄檢視可用來取得 DDL 觸發程序的相關資訊。  
  
 **取得 DDL 觸發程序引發所在之事件或事件群組的相關資訊**  
  
-   [sys.trigger_event_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-trigger-event-types-transact-sql)  
  
 **檢視觸發程序的相依性**  
  
-   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
-   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
-   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql)  
  
## <a name="database-scoped-ddl-triggers"></a>資料庫範圍的 DDL 觸發程序  
 **若要取得資料庫範圍觸發程序的相關資訊**  
  
-   [sys.triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql)  
  
 **若要取得引發觸發程序之資料庫事件的相關資訊**  
  
-   [sys.trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-trigger-events-transact-sql)  
  
 **若要檢視資料庫範圍觸發程序的定義**  
  
-   [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)  
  
 **若要取得 CLR 資料庫範圍觸發程序的相關資訊**  
  
-   [sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)  
  
## <a name="server-scoped-ddl-triggers"></a>伺服器範圍的 DDL 觸發程序  
 **若要取得伺服器範圍觸發程序的相關資訊**  
  
-   [sys.server_triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)  
  
 **若要取得引發觸發程序之伺服器事件的相關資訊**  
  
-   [sys.server_trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql)  
  
 **若要檢視伺服器範圍觸發程序的定義**  
  
-   [sys.server_sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql)  
  
 **若要取得 CLR 伺服器範圍觸發程序的相關資訊**  
  
-   [sys.server_assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)  
  
## <a name="see-also"></a>另請參閱  
 [DDL 觸發程序](../triggers/ddl-triggers.md)  
  
  
