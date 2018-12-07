---
title: 重新執行選項 (Distributed Replay 管理工具) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: d7bce6a5-d414-488d-a3cd-50c1c62019c4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 46285d61f38619ed8dff835faee266e5a76f591d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511162"
---
# <a name="replay-option-distributed-replay-administration-tool"></a>重新執行選項 (Distributed Replay 管理工具)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理工具 **DReplay.exe**是命令列工具，可用以與 Distributed Replay Controller 通訊。 此主題描述 **replay** 命令列選項與對應的語法。  
  
 **replay** 選項會起始事件重新執行階段，控制器在此階段中會分派重新執行資料給指定的用戶端、啟動分散式重新執行，並同步處理用戶端。 另外，參與重新執行的每個用戶端可以記錄重新執行活動，並在本機上儲存結果追蹤檔案。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") 如需管理工具語法所使用之語法慣例的詳細資訊，請參閱 [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
dreplay replay [-m controller] -d controller_working_dir [-o]  
    [-s target_server] -w clients [-c config_file]  
    [-f status_interval]  
```  
  
#### <a name="parameters"></a>參數  
 **-m** *controller*  
 指定控制器的電腦名稱。 您可以使用 "`localhost`" 或 "`.`" 表示本機電腦。  
  
 如果未指定 **-m** 參數，則會使用本機電腦。  
  
 **-d** *controller_working_dir*  
 指定控制器上儲存中繼檔案的目錄。 **-d** 是必要參數。  
  
 下列為適用需求：  
  
-   目錄必須位於控制器。  
  
-   您必須指定以磁碟機代號開頭的完整路徑 (例如 `c:\WorkingDir`)。  
  
-   路徑結尾不可以是反斜線 "`\`"。  
  
-   不支援 UNC 路徑。  
  
 **-o**  
 擷取用戶端的重新執行活動，並將其儲存在用戶端組態檔 `<ResultDirectory>` 中 `DReplayClient.xml`元素所指定的路徑中之結果追蹤檔案。  
  
 未指定 **-o** 參數時，不會產生結果追蹤檔案。 主控台輸出會在重新執行結尾時傳回摘要資訊，但不會提供其他重新執行統計資料。  
  
 **-s** *target_server*  
 指定分散式工作負載應該針對它重新執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目標執行個體。 您必須使用以下格式指定這個參數： **server_name[\instance name]**。  
  
 不可使用 "`localhost`" 或 "`.`" 當做目標伺服器。  
  
 如果在重新執行組態檔 **的** 區段中指定了 `<Server>` 元素，則不需要 `<ReplayOptions>` -s `DReplay.exe.replay.config`參數。  
  
 如果使用了 **-s** 參數，系統會忽略重新執行組態檔之 `<Server>` 區段中的 `<ReplayOptions>` 元素。  
  
 **-w** *clients*  
 此必要參數是以逗號分隔的清單 (不含空白)，會指定應該參與分散式重新執行之用戶端的電腦名稱。 不允許 IP 位址。 請注意，用戶端必須已經向控制器註冊。  
  
> [!NOTE]  
>  當用戶端服務啟動時，每個用戶端就會對用戶端組態檔中所指定的控制器進行註冊。  
  
 **-c** *config_file*  
 此為重新執行組態檔的完整路徑，用以指定不同於預設位置的儲存位置。  
  
 如果要使用重新執行組態檔 **的預設值，則不需要** -c `DReplay.exe.replay.config`參數。  
  
 **-f** *status_interval*  
 指定顯示狀態的頻率 (以秒計)。  
  
 如果未指定 **-f** ，則預設間隔為 30 秒。  
  
## <a name="examples"></a>範例  
 在此範例中，分散式重新執行會從修改過的重新執行組態檔 `DReplay.exe.replay.config`，衍生其大部分的行為。  
  
-   **-m** 參數會指定一個名為 `controller1` 的電腦，作為控制器。 當控制器服務執行於不同的電腦上時，必須指定電腦名稱。  
  
-   **-d** 參數會指定控制器上中繼檔案的位置， `c:\WorkingDir`。  
  
-   **-o** 參數會指定每個指定的用戶端擷取重新執行活動，並將其儲存至結果追蹤檔案。 注意：組態檔中的 `<ResultTrace>` 元素，可用以指定是否應記錄資料列計數與結果集。  
  
-   **-w** 參數會指定 `client1` 到 `client4` 的電腦，參與為分散式重新執行中的用戶端。  
  
-   **-c** 參數可用以指向修改過的組態檔 `DReplay.exe.replay.config`。  
  
-   不需要 **-s** 參數，因為重新執行組態檔 `<Server>` 的 `<ReplayOptions>` 元素中，指定了 `DReplay.exe.replay.config`元素。  
  
 從不同於控制器的電腦執行管理工具時，使用下列語法起始事件重新執行階段：  
  
```  
dreplay replay -m controller1 -d c:\WorkingDir -o -w client1,client2,client3,client4 -c c:\DReplay.exe.replay.config  
```  
  
 若要指定同步順序模式， `<SequencingMode>` 檔案的 `DReplay.exe.replay.config` 元素要設為等於 `synchronization`值。 重新執行組態檔的 `<ResultTrace>` 區段要修改，以指定應該記錄資料列計數。 下列 XML 範例會示範這些變更：  
  
```  
<?xml version='1.0'?>  
<Options>  
    <ReplayOptions>  
        <Server>server_name\replay_target_instance</Server>  
        <SequencingMode>synchronization</SequencingMode>  
        <ConnectTimeScale></ConnectTimeScale>  
        <ThinkTimeScale></ThinkTimeScale>  
        <HealthmonInterval>60</HealthmonInterval>  
        <QueryTimeout>3600</QueryTimeout>  
        <ThreadsPerClient></ThreadsPerClient>  
    </ReplayOptions>  
    <OutputOptions>  
        <ResultTrace>  
            <RecordRowCount>Yes</RecordRowCount>  
            <RecordResultSet>No</RecordResultSet>  
        </ResultTrace>  
    </OutputOptions>  
</Options>  
```  
  
 若要指定壓力順序模式， `<SequencingMode>` 檔案的 `DReplay.exe.replay.config` 元素要設為等於 `stress`值。 `<ConnectTimeScale>` 和 `<ThinkTimeScale>` 元素設為 `50` 值 (以指定 50%)。 如需有關連接時間和思考時間的詳細資訊，請參閱 [設定 Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)。 下列 XML 範例會示範這些變更：  
  
```  
<?xml version='1.0'?>  
<Options>  
    <ReplayOptions>  
        <Server>server_name\replay_target_instance_name</Server>  
        <SequencingMode>stress</SequencingMode>  
        <ConnectTimeScale>50</ConnectTimeScale>  
        <ThinkTimeScale>50</ThinkTimeScale>  
        <HealthmonInterval>60</HealthmonInterval>  
        <QueryTimeout>3600</QueryTimeout>  
        <ThreadsPerClient></ThreadsPerClient>  
    </ReplayOptions>  
    <OutputOptions>  
        <ResultTrace>  
            <RecordRowCount>Yes</RecordRowCount>  
            <RecordResultSet>No</RecordResultSet>  
        </ResultTrace>  
    </OutputOptions>  
</Options>  
```  
  
## <a name="permissions"></a>[權限]  
 您必須以互動使用者、本機使用者或網域使用者帳戶來執行管理工具。 若要使用本機使用者帳戶，管理工具和控制器必須在同一部電腦上執行。  
  
 如需詳細資訊，請參閱 [Distributed Replay 安全性](../../tools/distributed-replay/distributed-replay-security.md)。  
  
## <a name="see-also"></a>另請參閱  
 [重新執行追蹤資料](../../tools/distributed-replay/replay-trace-data.md)   
 [檢閱重新執行結果](../../tools/distributed-replay/review-the-replay-results.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [設定 Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)   
 [SQL Server Distributed Replay 論壇](https://social.technet.microsoft.com/Forums/sl/sqldru/)   
 [使用 Distributed Replay 對您的 SQL Server 進行負載測試 - 第 2 部分](https://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx)   
 [使用 Distributed Replay 對您的 SQL Server 進行負載測試 – 第 1 部分](https://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)  
  
  
