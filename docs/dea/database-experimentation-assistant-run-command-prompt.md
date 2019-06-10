---
title: SQL Server 升級的命令提示字元執行資料庫測試助理
description: 在命令提示字元中執行 資料庫測試助理
ms.custom: ''
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
manager: jroth
ms.openlocfilehash: c4603bf5fec8f1df8ae1e7fe0e711bf7b6e8f1e9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794428"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>在命令提示字元中執行 資料庫測試助理

本文說明如何使用 [命令提示字元] 視窗來擷取追蹤的資料庫測試助理 (DEA)，，然後再分析結果。 

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>使用 DEA 命令來啟動新的工作負載擷取

若要啟動新的工作負載擷取，請執行下列命令：

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**範例**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload"></a>重新執行工作負載

1.  Distributed Replay 控制器電腦登入。
2.  將轉換的工作負載追蹤擷取至 IRF 檔案使用 DEA 命令：

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3.  啟動追蹤擷取使用 StartReplayCaptureTrace.sql 執行 SQL Server 的目標電腦上。
       
    a.  在 SQL Server Management Studio (SSMS)，開啟 < Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql。
    
    b.  執行`Set @durationInMins=0`以便追蹤擷取指定的時間之後不會自動停止。
    
    c.  若要設定每個追蹤檔案的檔案大小上限，請執行`Set @maxfilesize`。 建議的大小為 200 （以 mb 為單位）。
    
    d.  編輯`@Tracefile`設定追蹤檔案的唯一名稱。
    
    e.  編輯`@dbname`來指定資料庫名稱，如果工作負載必須擷取只有在特定資料庫上。 根據預設，會擷取整部伺服器上的工作負載。 
4.  重新執行目標 SQL Server 執行個體 IRF 檔案：

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`
        
    a.  若要監視的狀態，請開啟 [命令提示字元] 視窗並執行`DReplay status -f 1`。
        
    b.  若要停止重新執行，例如，如果您看到傳遞 %低於預期，開啟 [命令提示字元] 視窗並執行`DReplay cancel`。

5.  停止追蹤擷取針對目標 SQL Server 執行個體。
6.  在 SSMS 中，開啟`<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`。
7.  編輯`@Tracefile`以符合執行 SQL Server 的目標電腦上的追蹤檔案路徑。
8.  針對執行 SQL Server 的目標電腦執行指令碼。

## <a name="analyze-traces-by-using-the-dea-command"></a>使用 DEA 命令分析追蹤

若要啟動新的追蹤分析，請執行下列命令：

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**範例**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="next-steps"></a>後續步驟

如需 19 分鐘簡介 DEA 和示範，觀看下列影片：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
