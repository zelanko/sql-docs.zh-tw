---
title: 前置處理選項 (Distributed Replay 管理工具) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 9b5012fd-233e-4a25-a2e1-585c63b70502
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ad198e96c24431ab51f0ab89517530598bfb1ced
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129438"
---
# <a name="preprocess-option-distributed-replay-administration-tool"></a>前置處理選項 (Distributed Replay 管理工具)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理工具 **DReplay.exe**是命令列工具，可用以與 Distributed Replay Controller 通訊。 本主題描述 **preprocess** 命令列選項與對應的語法。  
  
 **preprocess** 選項會起始前置處理階段。 在這個階段中，控制器會準備輸入追蹤資料，以便對目標伺服器重新執行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") 如需管理工具語法所使用之語法慣例的詳細資訊，請參閱 [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
dreplay preprocess [-m controller] -i input_trace_file  
    -d controller_working_dir [-c config_file] [-f status_interval]  
```  
  
#### <a name="parameters"></a>參數  
 **-m** _controller_  
 指定控制器的電腦名稱。 您可以使用 "`localhost`" 或 "`.`" 表示本機電腦。  
  
 如果未指定 **-m** 參數，則會使用本機電腦。  
  
 **-i** _input_trace_file_  
 指定控制器上輸入追蹤檔案的完整路徑，例如 `D:\Mytrace.trc`。 **-i** 是必要參數。  
  
 如果相同的目錄中存在換用檔案，系統就會自動載入並使用它們。 這些檔案必須遵循檔案換用命名慣例，例如：`Mytrace.trc`、`Mytrace_1.trc`、`Mytrace_2.trc`、`Mytrace_3.trc`... `Mytrace_n.trc`。  
  
> [!NOTE]  
>  如果您要在控制器以外的電腦上使用管理工具，就必須將輸入追蹤檔案複製到控制器，以便針對此參數使用本機路徑。  
  
 **-d** _controller_working_dir_  
 指定控制器上儲存中繼檔案的目錄。 **-d** 是必要參數。  
  
 下列為適用需求：  
  
-   目錄必須位於控制器。  
  
-   您必須指定以磁碟機代號開頭的完整路徑 (例如 `c:\WorkingDir`)。  
  
-   路徑結尾不可以是反斜線 "`\`"。  
  
-   不支援 UNC 路徑。  
  
 **-c** _config_file_  
 這是前置處理組態檔的完整路徑，用來指定儲存在不同位置之前置處理組態檔的位置。 此參數可以是 UNC 路徑，也可以位於您執行管理工具所在之電腦的本機。  
  
 如果不需要篩選，或您不想要修改最大閒置時間，則不需要 **-c** 參數。  
  
 如果沒有 **-c** 參數，則會使用預設前置處理組態檔 `DReplay.exe.preprocess.config`。  
  
 **-f** _status_interval_  
 指定顯示狀態訊息的頻率 (以秒為單位)。  
  
 如果未指定 **-f** ，則預設間隔為 30 秒。  
  
## <a name="examples"></a>範例  
 在此範例中，前置處理階段是使用所有預設設定來起始。 `localhost` 值指出控制器服務與管理工具在同一部電腦上執行。 *input_trace_file* 參數會指定輸入追蹤資料的位置 `c:\mytrace.trc`。 因為沒有涉及任何追蹤檔案篩選，所以必須指定 **-c** 參數。  
  
```  
dreplay preprocess -m localhost -i c:\mytrace.trc -d c:\WorkingDir  
```  
  
 在此範例中，已起始前置處理階段，而且已指定修改的前置處理組態檔。 與上個範例不同的是，如果您將修改過的組態檔儲存在不同的位置，就會使用 **-c** 參數來指向該組態檔。 例如：  
  
```  
dreplay preprocess -m localhost -i c:\mytrace.trc -d c:\WorkingDir -c c:\DReplay.exe.preprocess.config  
```  
  
 在修改的前置處理組態檔中，加入了一個篩選條件，它會在分散式重新執行期間篩選出系統工作階段。 此篩選是透過修改前置處理組態檔 `<PreprocessModifiers>` 中的 `DReplay.exe.preprocess.config`元素來加入。  
  
 下面將顯示已修改組態檔的範例：  
  
```  
<?xml version='1.0'?>  
<Options>  
    <PreprocessModifiers>  
        <IncSystemSession>No</IncSystemSession>  
        <MaxIdleTime>-1</MaxIdleTime>  
    </PreprocessModifiers>  
</Options>  
```  
  
## <a name="permissions"></a>[權限]  
 您必須以互動使用者、本機使用者或網域使用者帳戶來執行管理工具。 若要使用本機使用者帳戶，管理工具和控制器必須在同一部電腦上執行。  
  
 如需詳細資訊，請參閱 [Distributed Replay 安全性](../../tools/distributed-replay/distributed-replay-security.md)。  
  
## <a name="see-also"></a>另請參閱  
 [準備輸入追蹤資料](../../tools/distributed-replay/prepare-the-input-trace-data.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [設定 Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
