---
description: 取得 DDL 觸發程序的詳細資訊
title: 取得 DDL 觸發程序的資訊 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 74380279e43df3165343e89754c1b124a0ef9363
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418912"
---
# <a name="get-information-about-ddl-triggers"></a>取得 DDL 觸發程序的詳細資訊
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  本章節所列的目錄檢視可用來取得 DDL 觸發程序的相關資訊。  
  
 **取得 DDL 觸發程序引發所在之事件或事件群組的相關資訊**  
  
-   [sys.trigger_event_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-event-types-transact-sql.md)  
  
 **檢視觸發程序的相依性**  
  
-   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
-   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)  
  
-   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
## <a name="database-scoped-ddl-triggers"></a>資料庫範圍的 DDL 觸發程序  
 **若要取得資料庫範圍觸發程序的相關資訊**  
  
-   [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
 **若要取得引發觸發程序之資料庫事件的相關資訊**  
  
-   [sys.trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)  
  
 **若要檢視資料庫範圍觸發程序的定義**  
  
-   [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)  
  
 **若要取得 CLR 資料庫範圍觸發程序的相關資訊**  
  
-   [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)  
  
## <a name="server-scoped-ddl-triggers"></a>伺服器範圍的 DDL 觸發程序  
 **若要取得伺服器範圍觸發程序的相關資訊**  
  
-   [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)  
  
 **若要取得引發觸發程序之伺服器事件的相關資訊**  
  
-   [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)  
  
 **若要檢視伺服器範圍觸發程序的定義**  
  
-   [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)  
  
 **若要取得 CLR 伺服器範圍觸發程序的相關資訊**  
  
-   [sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [DDL 觸發程序](../../relational-databases/triggers/ddl-triggers.md)  
  
  
