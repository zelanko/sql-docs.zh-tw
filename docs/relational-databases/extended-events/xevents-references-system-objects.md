---
title: XEvent 相關系統物件
ms.date: 03/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jukoesma
ms.technology: xevents
ms.topic: reference
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 38982119f9c4485d99263a53c73d1e1c1e4404dc
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287732"
---
# <a name="system-objects-that-support-extended-events"></a>支援擴充事件的系統物件

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

現有的文章會提供與擴充事件相關之其他文章的連結。 這些文章會描述下列內容：

- 提供擴充事件功能支援的系統物件。
- SQL Server 本身會使用擴充事件的部分。
- 位於雲端之 Azure SQL Database 特定的擴充事件層面。

此清單並不一定是完整的。

## <a name="system-tables"></a>系統資料表

- [擴充事件資料表 - trace_xe_action_map](../system-tables/extended-events-tables-trace-xe-action-map.md)

- [擴充事件資料表 - trace_xe_event_map](../system-tables/extended-events-tables-trace-xe-event-map.md)

## <a name="system-catalog-views"></a>系統目錄檢視

- [擴充事件目錄檢視 (Transact-SQL)](../system-catalog-views/extended-events-catalog-views-transact-sql.md)

- [sys.server_event_sessions (Transact-SQL)](../system-catalog-views/sys-server-event-sessions-transact-sql.md)

- [sys.server_event_session_actions (Transact-SQL)](../system-catalog-views/sys-server-event-session-actions-transact-sql.md)

- [sys.server_event_session_events (Transact-SQL)](../system-catalog-views/sys-server-event-session-events-transact-sql.md)

- [sys.server_event_session_fields (Transact-SQL)](../system-catalog-views/sys-server-event-session-fields-transact-sql.md)

- [sys.server_event_session_targets (Transact-SQL)](../system-catalog-views/sys-server-event-session-targets-transact-sql.md)

## <a name="other-system-objects"></a>其他系統物件

- [擴充事件動態管理檢視](../system-dynamic-management-views/extended-events-dynamic-management-views.md)

## <a name="uses-of-extended-events-by-sql-server-itself"></a>擴充事件對 SQL Server 本身的用途

此清單並不完整。

- [存取擴充事件記錄檔中的診斷資訊](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)

- [設定 Always On 可用性群組的延伸事件](../../database-engine/availability-groups/windows/always-on-extended-events.md)

- [Stretch Database 的擴充事件](../../sql-server/stretch-database/extended-events-for-stretch-database.md)

## <a name="azure-sql-database-and-extended-events"></a>Azure SQL Database 和擴充事件

- [Azure SQL Database 中的擴充事件](/azure/sql-database/sql-database-xevent-db-diff-from-svr)

- [sys.database_event_session_targets (Azure SQL Database)](../system-catalog-views/sys-database-event-session-targets-azure-sql-database.md)

- [sys.database_event_session_fields (Azure SQL Database)](../system-catalog-views/sys-database-event-session-fields-azure-sql-database.md)

- [sys.database_event_session_events (Azure SQL Database)](../system-catalog-views/sys-database-event-session-events-azure-sql-database.md)

- [sys.database_event_session_actions (Azure SQL Database)](../system-catalog-views/sys-database-event-session-actions-azure-sql-database.md)
