---
description: MSSQLSERVER_3023
title: MSSQLSERVER_3023
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3023 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 0197c7e5b75164615572e4041a5b348a4d5abcc4
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418686"
---
# <a name="mssqlserver_3023"></a>MSSQLSERVER_3023
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細資料

|屬性|值|
|---|---|
|產品名稱|SQL Server|
|事件識別碼|3023|
|事件來源|MSSQLSERVER|
|元件|SQLEngine|
|符號名稱|DB_IN_USE_DUMP|
|訊息文字|資料庫上的備份與檔案操作作業 (例如 ALTER DATABASE ADD FILE) 必須進行序列化。 請在目前的備份或檔案操作作業完成之後，重新發出陳述式|
||

## <a name="explanation"></a>說明

您嘗試在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行備份、壓縮或更改資料庫命令，並遇到下列訊息：

> 訊息 3023，層級 16，狀態 2，第 1 行  
資料庫上的備份與檔案操作作業 (例如 ALTER DATABASE ADD FILE) 必須進行序列化。 請在目前的備份或檔案操作作業完成之後，重新發出陳述式。

> 訊息 3013，層級 16，狀態 1，第 1 行  
備份資料庫正在異常結束。

此外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔包含類似下列的訊息：

> \<Datetime> 備份錯誤：3041，嚴重性：16，狀態：1。  
\<Datetime> 備份 BACKUP 無法完成 BACKUP DATABASE MyDatabase WITH DIFFERENTIAL 命令。 詳細訊息請檢查備份應用程式記錄檔。

您可能也會注意到，當從各種動態管理檢視 (DMV) (例如從 `sys.dm_exec_requests` 或 `sys.dm_os_waiting_tasks`) 查看這些命令的狀態時，這些命令會發生 `wait_type = LCK_M_U` 與 `wait_resource = DATABASE: <id> [BULKOP_BACKUP_DB]`。

## <a name="possible-causes"></a>可能的原因

當完整資料庫正在針對資料庫作業時，有幾項規則會允許或不允許作業進行。 部分範例如下：

- 每次只能有一個資料備份 (當進行完整資料庫備份時，則不可同時進行差異備份或增量備份)。
- 每次只能進行一個記錄備份 (當進行完整資料庫備份時，允許進行記錄備份)。
- 當備份正在進行時，您無法在資料庫中新增或卸除檔案。
- 當資料庫備份正在進行時，您無法壓縮檔案。
- 當備份正在進行時，可進行有限度的復原模式變更。

當執行任何一項這類會產生衝突的作業時，命令會發生＜說明＞一節中所述的鎖定等候，且您會收到 3023 與 3041 訊息。

## <a name="user-action"></a>使用者動作

檢查各種資料庫維護活動的排程，然後調整排程，讓這些作業或命令不會互相衝突。

## <a name="more-information"></a>詳細資訊

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會記錄備份在 `msdb` 資料庫中的開始時間與結束時間。 您可檢查備份歷程記錄，以判斷在嘗試進行增量備份時，是否正同時進行完整資料庫備份，因而導致錯誤。 您可使用下列查詢來協助處理程序：

```sql
select database_name, type, backup_start_date, backup_finish_date
from msdb.dbo.backupset
order by database_name, type, backup_start_date, backup_finish_date
go
```

您也可以使用 SQL Profiler 追蹤中的 **使用者錯誤訊息** 事件，或擴充事件中的 **error_reported** 事件，從 3023 訊息的報告，追溯回開始備份或其他維護命令的應用程式。
