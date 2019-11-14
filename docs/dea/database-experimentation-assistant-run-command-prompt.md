---
title: 在命令提示字元中執行資料庫測試助理
description: 在命令提示字元中執行資料庫測試助理
ms.custom: seo-lt-2019
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: c3b87eafa460cfef69666a3837f56626dab81d47
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056568"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt-sql-server"></a>在命令提示字元中執行資料庫測試助理（SQL Server）

本文說明如何使用 [命令提示字元] 視窗，以資料庫測試助理（DEA）來捕捉追蹤，然後分析結果。 

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>使用 DEA 命令來啟動新的工作負載捕獲

若要啟動新的工作負載捕獲，請執行下列命令：

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**範例**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload"></a>重新執行工作負載

1.  登入 Distributed Replay 控制器電腦。
2.  使用 DEA 命令，將您所捕捉的工作負載追蹤轉換成 IRF 檔案：

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3.  使用 StartReplayCaptureTrace 在執行 SQL Server 的目的電腦上啟動追蹤捕捉。
       
    a.  在 SQL Server Management Studio （SSMS）中，開啟 < Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql。
    
    b.  執行 `Set @durationInMins=0`，讓追蹤捕捉不會在指定的時間後自動停止。
    
    c.  若要設定每個追蹤檔案的檔案大小上限，請執行 `Set @maxfilesize`。 建議的大小為200（以 MB 為單位）。
    
    d.  編輯 `@Tracefile`，為您的追蹤檔案設定唯一的名稱。
    
    E.  如果工作負載必須只在特定資料庫上進行捕獲，請編輯 `@dbname` 以指定資料庫名稱。 根據預設，會捕獲整個伺服器上的工作負載。 
4.  針對目標 SQL Server 實例重新執行 IRF 檔案：

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`
        
    a.  若要監視狀態，請開啟 [命令提示字元] 視窗，然後執行 `DReplay status -f 1`。
        
    b.  若要停止重新執行，例如，如果您看到 pass% 低於預期，請開啟 [命令提示字元] 視窗，然後執行 `DReplay cancel`。

5.  停止目標 SQL Server 實例上的追蹤捕捉。
6.  在 SSMS 中，開啟 `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`。
7.  編輯 `@Tracefile` 以符合執行 SQL Server 之目的電腦上的追蹤檔案路徑。
8.  針對執行 SQL Server 的目的電腦執行腳本。

## <a name="analyze-traces-by-using-the-dea-command"></a>使用 DEA 命令來分析追蹤

若要啟動新的追蹤分析，請執行下列命令：

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**範例**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="next-steps"></a>後續的步驟

如需 DEA 和示範的19分鐘簡介，請觀看下列影片：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
