---
title: 在命令提示字元中執行資料庫測試助理
description: 在命令提示字元中執行資料庫測試助理
ms.custom: seo-lt-2019
ms.date: 02/25/2020
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: 674f40b16437547956178293c5b491b11c8b2f89
ms.sourcegitcommit: d973b520f387b568edf1d637ae37d117e1d4ce32
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85215485"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>在命令提示字元中執行資料庫測試助理

本文說明如何在資料庫測試助理（DEA）中捕捉追蹤，然後從命令提示字元分析結果。

   > [!NOTE]
   > 若要深入瞭解每個 DEA 作業，請嘗試執行下列命令：
   >
   > `Deacmd.exe -o <operation> --help`
   >
   > 需要作業名稱;有效的作業包括**分析**、 **StartCapture**和**StopCapture**。

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>使用 DEA 命令來啟動新的工作負載捕獲

若要啟動新的工作負載捕獲，請在命令提示字元中執行下列命令：

`Deacmd.exe -o StartCapture -n <Trace FileName> -x <Trace Format> -h <SQLServerInstance> -f <database name> -e <Encrypt Connection> -m <Authetication Mode> -u <user name> -p <password> -l <Location of Output Folder> -d <duration>`

**範例**

`Deacmd.exe -o StartCapture -n sql2008capture -x 0 -h localhost -f adventureworks -e --trust -m 0 -l c:\test  -d 60`

**其他選項**

使用命令啟動新的工作負載捕捉時 `Deacmd.exe` ，您可以使用下列其他選項：

| 選項| 描述 |  
| --- | --- |
| -n, --name | 具備追蹤檔案名 |
| -x，--format | 具備追蹤的格式（Trace = 0，XEvents = 1） |
| -d，--duration | 具備捕捉的最大持續時間（以分鐘為單位） |
| -l, --location | 具備在主機電腦上儲存追蹤/xevent 檔案的輸出檔案夾位置 |
| -t，--類型 | （預設值：0） Sql Server 的類型/版本（SqlServer = 0，AzureSQLDB = 1，Azure SQL 受控執行個體 = 2） |
| -h, --host | 具備SQL Server 主機名稱和/或實例名稱，以開始捕獲 |
| -e、--encrypt | （預設值： True）SQL Server 實例的加密連接。 預設值為 true。 |
| --信任 | （預設值： False）連接到 SQL Server 實例時，信任伺服器憑證。 預設值為 false。 |
| -f、--databasename | （預設值：）要篩選追蹤的資料庫名稱，如果未指定，則會在所有資料庫上啟動 capture |
| -m、--authmode | （預設值：0）驗證模式（Windows = 0，Sql 驗證 = 1） |
| -u、--username | 用來連接到 SQL Server 的使用者名稱 |
| -p、--password | 用來連接到 SQL Server 的密碼 |

## <a name="replay-a-workload-capture"></a>重新執行工作負載捕獲

**使用 Distributed Replay**

如果您使用的是 Distributed Replay，請執行下列步驟。

1. 登入 Distributed Replay 控制器電腦。
2. 若要將使用 DEA 命令所捕獲的工作負載追蹤轉換成 IRF 檔案，請在命令提示字元中執行下列命令：

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3. 使用 StartReplayCaptureTrace 在執行 SQL Server 的目的電腦上啟動追蹤捕捉。

    a.  在 SQL Server Management Studio （SSMS）中，開啟 <Dea_InstallPath \> \Scripts\StartReplayCaptureTrace.sql。

    b.  執行， `Set @durationInMins=0` 讓追蹤捕捉不會在指定的時間後自動停止。

    c.  若要設定每個追蹤檔案的檔案大小上限，請執行 `Set @maxfilesize` 。 建議的大小為200（以 MB 為單位）。

    d.  編輯 `@Tracefile` ，為您的追蹤檔案設定唯一的名稱。

    e.  `@dbname`如果工作負載必須只在特定資料庫上進行捕獲，請編輯以指定資料庫名稱。 根據預設，會捕獲整個伺服器上的工作負載。

4. 若要針對目標 SQL Server 實例重新執行 IRF 檔，請在命令提示字元中執行下列命令：

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`

    a.  若要監視狀態，請在命令提示字元中執行 `DReplay status -f 1` 。

    b.  若要停止重新執行，例如，如果您看到 pass% 低於預期，請在命令提示字元中執行 `DReplay cancel` 。

5. 停止目標 SQL Server 實例上的追蹤捕捉。
6. 在 SSMS 中，開啟 `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql` 。
7. [編輯] `@Tracefile` 以符合執行 SQL Server 之目的電腦上的追蹤檔案路徑。
8. 針對執行 SQL Server 的目的電腦執行腳本。

**使用內建重新執行**

如果您使用內建重新執行，則不需要設定 Distributed Replay。 您可以透過命令列使用內建重新執行功能，但在過渡期間，您可以使用我們的 GUI，使用內建的重新執行來執行重新播放。

## <a name="analyze-traces-using-the-dea-command"></a>使用 DEA 命令來分析追蹤

若要開始新的追蹤分析，請在命令提示字元中執行下列命令：

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -h <SQLserverInstance> -e <encryptconnection> -u <username>`

**範例**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -h localhost -e`

若要查看這些追蹤檔案的分析報表，您需要使用 GUI 來查看圖表和組織的計量。  不過，分析資料庫會寫入至指定的 SQL Server 實例，因此您也可以直接查詢產生的分析資料表。

**其他選項**

使用 DEA 命令分析追蹤時，您可以使用下列其他選項：

| 選項| 描述 |  
| --- | --- |
| -a、--traceA | 具備實例之事件檔案的檔案路徑。 範例 C:\traces\Sql2008trace.trc。  如果有一批次檔，請選取第一個檔案，DEA 會自動檢查換用檔案。 如果檔案是在 blob 中，請提供您想要在本機儲存事件檔案的資料夾路徑。  範例 C:\traces\ |
| -b，--traceB | 具備B 實例之事件檔案的檔案路徑。 範例 C:\traces\Sql2014trace.trc。 如果有一批次檔，請選取第一個檔案，DEA 會自動檢查換用檔案。 如果檔案是在 blob 中，請提供您想要在本機儲存事件檔案的資料夾路徑。  範例 C:\traces\ |
| -r、--ReportName | 具備目前分析的名稱。 產生的分析報表將會以這個名稱來識別。 |
| -t，--類型 | （預設值：0） Sql Server 的類型/版本（SqlServer = 0，AzureSQLDB = 1，Azure SQL 受控執行個體 = 2） |
| -h, --host | 具備SQL Server 主機名稱和（或）實例名稱 |
| -e、--encrypt | （預設值： True）SQL Server 實例的加密連接。 預設值為 true。 |
| --信任 | （預設值： False）連接到 SQL Server 實例時，信任伺服器憑證。 預設值為 false。 |
| -m、--authmode | （預設值：0）驗證模式（Windows = 0，Sql 驗證 = 1） |
| -u、--username | 用來連接到 SQL Server 的使用者名稱 |
| --p | 用來連接到 SQL Server 的密碼 |
| --ab | （預設值： False）追蹤 A 的儲存位置是在 blob 中。 若已使用，也必須指定--阿布達比（追蹤 Blob Url） |
| --bb | （預設值： False）追蹤 B 的儲存位置在 blob 中。 若使用，則必須同時指定--bbu （追蹤 B Blob Url） |
| --阿布達比 | 具有 SAS 金鑰之實例的 Blob URL |
| --bbu | 具有 SAS 金鑰的 B 實例 Blob URL |

## <a name="see-also"></a>另請參閱

- 如需使用 DEA 的詳細資訊，請參閱[資料庫測試助理的總覽](database-experimentation-assistant-overview.md)。
