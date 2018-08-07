---
title: 使用 SSMS XEvent 分析工具 | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
author: yualan
ms.author: alayu
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: bcb53b0d9e6254d00ed313ba6df2774810eb9344
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39555468"
---
# <a name="use-the-ssms-xevent-profiler"></a>使用 SSMS XEvent 分析工具
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
XEvent 分析工具是一項 SQL Server Management Studio (SSMS) 功能，其可顯示擴充事件的即時檢視器視窗。 本概觀將說明使用此分析工具的理由、重要功能，並會提供檢視擴充事件的入門指示。

## <a name="why-would-i-use-the-xevent-profiler"></a>為什麼要使用 XEvent 分析工具？
XEvent 分析工具不同於 SQL Profiler，其可直接整合到 SSMS，並以 SQL 引擎中可調式擴充事件技術作為基礎建置而成。 您可利用這項功能在 SQL 伺服器上快速存取診斷事件的即時串流檢視。 您可自訂此檢視，讓這些自訂內容以 .viewsettings 檔案的形式與其他 SSMS 使用者共用。 XE 分析工具建立的工作階段，對運作中 SQL 伺服器所造成的干擾，低於類似 SQL 追蹤使用 SQL Profiler 所造成的干擾。 使用者也可使用現有的 XE 工作階段屬性 UI 或是 TSQL，自訂此工作階段。

## <a name="prerequisites"></a>Prerequisites
只有 SQL Server Management Studio (SSMS) v17.3 或更新版本才提供此功能。 請確認目前使用的是最新版本。 您可以於[這裡](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)找到最新版本。

## <a id="getting-started"></a>使用者入門
若要存取 XEvent 分析工具，請遵循下列步驟進行：

1. 開啟 [SQL Server Management Studio]。

2. 連線至 SQL Server 資料庫引擎或 localhost 的執行個體。

3. 在物件總管中找到 XE 分析工具功能表項目，然後按一下 '+' 符號將其展開。

   ![XEProfiler 功能表](media/xevents-xe-profiler-menu.png)

4. 若想檢視此工作階段中的所有擴充事件，請按兩下 [標準]。 若想要檢視記錄的 SQL 陳述式，請按一下 [T-SQL]。 若尚未建立工作階段，就會為您建立工作階段。

   ![XEProfiler 工作階段](media/xevents-xe-profiler-start-session.png)

5. 現在即可檢視擴充事件。

   ![XEProfiler 檢視器](media/xevents-xe-profiler-start-viewer.png)

## <a name="see-also"></a>另請參閱
[擴充事件](../../relational-databases/extended-events/extended-events.md)  
[擴充事件工具](../../relational-databases/extended-events/extended-events-tools.md)  
  
  
