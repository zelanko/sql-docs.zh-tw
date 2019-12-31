---
title: 在命令提示字元中執行資料庫測試助理
description: 在命令提示字元中執行資料庫測試助理
ms.custom: seo-lt-2019
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: f5a0f7441dd17aec2587c772a678a3681fd3b423
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74317725"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>在命令提示字元中執行資料庫測試助理

本文說明如何在資料庫測試助理（DEA）中捕捉追蹤，然後從命令提示字元分析結果。

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>使用 DEA 命令來啟動新的工作負載捕獲

若要啟動新的工作負載捕獲，請在命令提示字元中執行下列命令：

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**實例**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload-capture"></a>重新執行工作負載捕獲

1. 登入 Distributed Replay 控制器電腦。
2. 若要將使用 DEA 命令所捕獲的工作負載追蹤轉換成 IRF 檔案，請在命令提示字元中執行下列命令：

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3. 使用 StartReplayCaptureTrace 在執行 SQL Server 的目的電腦上啟動追蹤捕捉。

    a.  在 SQL Server Management Studio （SSMS）中，開啟 <\>Dea_InstallPath \Scripts\StartReplayCaptureTrace.sql。

    b.  執行`Set @durationInMins=0` ，讓追蹤捕捉不會在指定的時間後自動停止。

    c.  若要設定每個追蹤檔案的檔案大小上限`Set @maxfilesize`，請執行。 建議的大小為200（以 MB 為單位）。

    d.  編輯`@Tracefile` ，為您的追蹤檔案設定唯一的名稱。

    e.  如果`@dbname`工作負載必須只在特定資料庫上進行捕獲，請編輯以指定資料庫名稱。 根據預設，會捕獲整個伺服器上的工作負載。

4. 若要針對目標 SQL Server 實例重新執行 IRF 檔，請在命令提示字元中執行下列命令：

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`

    a.  若要監視狀態，請在命令提示字元中`DReplay status -f 1`執行。

    b.  若要停止重新執行，例如，如果您看到 pass% 低於預期，請在命令提示字元中執行`DReplay cancel`。

5. 停止目標 SQL Server 實例上的追蹤捕捉。
6. 在 SSMS 中， `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`開啟。
7. [ `@Tracefile`編輯] 以符合執行 SQL Server 之目的電腦上的追蹤檔案路徑。
8. 針對執行 SQL Server 的目的電腦執行腳本。

## <a name="analyze-traces-using-the-dea-command"></a>使用 DEA 命令來分析追蹤

若要開始新的追蹤分析，請在命令提示字元中執行下列命令：

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**實例**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="see-also"></a>另請參閱

- 如需使用 DEA 的詳細資訊，請參閱[資料庫測試助理的總覽](database-experimentation-assistant-overview.md)。
