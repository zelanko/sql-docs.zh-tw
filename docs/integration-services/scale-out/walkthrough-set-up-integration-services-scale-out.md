---
title: 逐步解說：設定 SSIS Scale Out | Microsoft Docs
description: 本文將引導您完成 SSIS Scale Out 的安裝和設定
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
author: HaoQian-MS
ms.author: haoqian
ms.openlocfilehash: c1f2a7670913f2df948201b29f26e0283f27f698
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79288742"
---
# <a name="walkthrough-set-up-integration-services-ssis-scale-out"></a>逐步解說：設定 Integration Services (SSIS) Scale Out

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


完成下列工作，以設定 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] (SSIS) Scale Out。 

> [!TIP]
> 如果您要在一部電腦上安裝 Scale Out，請同時安裝 Scale Out Master 和 Scale Out Worker 功能。 當您同時安裝這些功能時，會自動產生端點，以連接至擴增主機。 

* [安裝擴增主機](#InstallMaster)

* [安裝擴增背景工作](#InstallWorker)

* [安裝擴增背景工作用戶端憑證](#InstallCert)

* [開啟防火牆通訊埠](#Firewall)

* [啟動 SQL Server 擴增主機和背景工作服務](#Start)

* [啟用擴增主機](#EnableMaster)

* [啟用 SQL Server 驗證模式](#EnableAuth)

* [啟用擴增背景工作](#EnableWorker)

## <a name="InstallMaster"></a> 安裝擴增主機

若要設定 Scale Out Master，您必須在設定 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 時安裝 Database Engine Services、[!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 以及 SSIS 的 Scale Out Master 功能。 

如需設定 Database Engine 和 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 的資訊，請參閱[安裝 SQL Server Database Engine](../../database-engine/install-windows/install-sql-server-database-engine.md) 和[安裝 Integration Services](../install-windows/install-integration-services.md)。

> [!NOTE]
> 若要使用預設 SQL Server 驗證帳戶進行 Scale Out 記錄，請在資料庫引擎安裝期間，於 [資料庫引擎設定]  頁面上選取 [混合模式] 作為驗證模式。 如需詳細資訊，請參閱[變更擴增記錄的帳戶](change-logdb-account.md)。

若要安裝 Scale Out Master 功能，請使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈或命令提示字元。

### <a name="install-scale-out-master-with-the-sql-server-installation-wizard"></a>使用 SQL Server 安裝精靈安裝 Scale Out Master
1.  在 [特徵選取]  頁面上，選取列在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 下方的 [擴增主機]  。   
  
    ![特徵選取主要](media/feature-select-master.PNG)
  
2.  在 [伺服器組態]  頁面上，選取要執行 [SQL Server Integration Services 擴增主機服務]  的帳戶，然後選取 [啟動類型]  。  
    ![伺服器組態](media/server-config.PNG)

3.  在 [Integration Services 擴增主機組態]  頁面上，指定擴增主機用來與擴增背景工作通訊的通訊埠編號。 預設通訊埠編號是 8391。  

    ![主機組態](media/master-config.PNG "主機設定")

4.  執行下列其中一項，以指定用來保護擴增主機與擴增背景工作間之通訊的 SSL 憑證。
    * 按一下 [建立新的 SSL 憑證]  ，讓安裝程序建立預設自我簽署 SSL 憑證。  預設憑證會安裝到 [受信任的根憑證授權單位] 的 [本機電腦] 下方。 您可以在此憑證中指定 CN。 主要端點的主機名稱應該併入 CN 中。 預設會包含 Master 節點的電腦名稱和 IP。
    * 按一下 [使用現有的 SSL 憑證]  ，然後按一下 [瀏覽]  選取憑證，以選取本機電腦上的現有 SSL 憑證。 憑證的指紋會出現在文字方塊中。 按一下 [瀏覽]  會顯示在 [受信任的根憑證授權單位] 的 [本機電腦] 中所儲存的憑證。 您選取的憑證必須儲存在這裡。       

    ![主機組態 2](media/master-config-2.PNG "主機組態 2")
  
5.  完成 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈。

### <a name="install-scale-out-master-from-the-command-prompt"></a>從命令提示字元安裝 Scale Out Master

請遵循 [從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)中的指示進行。 執行下列動作，以設定 Scale Out Master 的參數：
 
1.  將 `IS_Master` 新增至參數 `/FEATURES`

2.  指定下列參數和其值，以設定 Scale Out Master：
    -   `/ISMASTERSVCACCOUNT`
    -   `/ISMASTERSVCPASSWORD`
    -   `/ISMASTERSVCSTARTUPTYPE`
    -   `/ISMASTERSVCPORT`
    -   `/ISMasterSVCSSLCertCN` (選擇性)
    -   `/ISMASTERSVCTHUMBPRINT` (選擇性)

    > [!NOTE]
    > 如果 Scale Out Master 未與資料庫引擎一起安裝，而且資料庫引擎執行個體是一個具名執行個體，則您需要在安裝之後於 Scale Out Master 服務設定檔中設定 `SqlServerName`。 如需詳細資訊，請參閱 [Scale Out Master](integration-services-ssis-scale-out-master.md)。

## <a name="InstallWorker"></a> 安裝擴增背景工作
 
若要設定 Scale Out Worker，您必須在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝時安裝 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 和其 Scale Out Worker 功能。

若要安裝 Scale Out Worker 功能，請使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈或命令提示字元。

### <a name="install-scale-out-worker-with-the-sql-server-installation-wizard"></a>使用 SQL Server 安裝精靈安裝 Scale Out Worker

1.  在 [特徵選取]  頁面上，選取列在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 下方的 [擴增背景工作]  。

    ![特徵選取背景工作](media/feature-select-worker.PNG)

2.  在 [伺服器組態]  頁面上，選取要執行 [SQL Server Integration Services 擴增背景工作服務]  的帳戶，然後選取 [啟動類型]  。

    ![伺服器組態 2](media/server-config-2.PNG "伺服器組態 2")

3.  在 [Integration Services 擴增背景工作組態]  頁面上，指定連接至擴增主機的端點。 

    - 針對**單一電腦**環境，同時安裝 Scale Out Master 和 Scale Out Worker 時，即會自動產生端點。 

    - 針對**多部電腦**環境，端點包含已安裝 Scale Out Master 之電腦的名稱或 IP，以及 Scale Out Master 安裝期間所指定的連接埠號碼。
   
    ![背景工作組態 1](media/worker-config.PNG "背景工作組態 1")    

    > [!NOTE]
    > 您可以在這裡略過背景工作節點設定，並在安裝之後使用 [Scale Out Manager](integration-services-ssis-scale-out-manager.md) 建立 Scale Out Worker 與 Scale Out Master 的關聯。

4. 針對**多部電腦**環境，指定用來驗證 Scale Out Master 的用戶端 SSL 憑證。 針對**單一電腦**環境中，您不需要指定用戶端 SSL 憑證。 
  
    按一下 [瀏覽]  找出憑證檔案 (*.cer)。 若要使用預設 SSL 憑證，請選取 Scale Out Master 安裝所在電腦的 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn` 下方的 `SSISScaleOutMaster.cer` 檔案。   

    ![背景工作組態 2](media/worker-config-2.PNG "背景工作組態 2")

    > [!NOTE]
    > 自我簽署 Scale Out Master 所使用的 SSL 憑證時，需要在具有 Scale Out Worker 的電腦上安裝對應的用戶端 SSL 憑證。 如果您在 [Integration Services 擴增背景工作設定]  頁面上提供用戶端 SSL 憑證的檔案路徑，則會自動安裝憑證；否則，您稍後必須手動安裝憑證。 
     
5. 完成 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 安裝精靈。

### <a name="install-scale-out-worker-from-the-command-prompt"></a>從命令提示字元安裝 Scale Out Worker

請遵循 [從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)中的指示進行。 執行下列動作，以設定 Scale Out Worker 的參數：

1.  將 IS_Worker 新增至 `/FEATURES` 參數。

2. 指定下列參數和其值，以設定 Scale Out Worker：
    -   `/ISWORKERSVCACCOUNT`
    -   `/ISWORKERSVCPASSWORD`
    -   `/ISWORKERSVCSTARTUPTYPE`
    -   `/ISWORKERSVCMASTER` (選擇性)
    -   `/ISWORKERSVCCERT` (選擇性)
 
## <a name="InstallCert"></a> 安裝擴增背景工作用戶端憑證

在安裝 Scale Out Worker 期間，將會在電腦上自動建立和安裝背景工作憑證。 同時，會在 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn` 下方安裝對應的用戶端憑證 SSISScaleOutWorker.cer。 若要讓 Scale Out Master 驗證 Scale Out Worker，您必須將此用戶端憑證新增至具有 Scale Out Master 之本機電腦的根存放區。
  
若要將用戶端憑證新增至根存放區，請按兩下 .cer 檔案，然後按一下 [憑證] 對話方塊中的 [安裝憑證]  。 隨即開啟 [憑證匯入精靈]  。  

## <a name="Firewall"></a> 開啟防火牆通訊埠

在 Scale Out Master 電腦上，於 Windows 防火牆中，開啟在 Scale Out Master 安裝期間所指定的連接埠以及 SQL Server 的連接埠 (預設為 1433)。

> [!Note]
> 在您開啟防火牆連接埠之後，也需要重新啟動 Scale Out Worker 服務。
    
## <a name="Start"></a> 啟動 SQL Server 擴增主機和背景工作服務

如果您未在安裝期間將服務的啟動類型設定為 [自動]  ，請啟動下列服務：

-   SQL Server Integration Services Scale Out Master 14.0 (SSISScaleOutMaster140)

-   SQL Server Integration Services Scale Out Worker 14.0 (SSISScaleOutWorker140)

## <a name="EnableMaster"></a> 啟用擴增主機

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)] 中建立 SSISDB 目錄時，請選取 [建立目錄]  對話方塊中的 [啟用此伺服器作為 SSIS 擴增主機]  。

建立目錄之後，您可以使用 [Scale Out Manager](integration-services-ssis-scale-out-manager.md) 來啟用 Scale Out Master。

## <a name="EnableAuth"></a> 啟用 SQL Server 驗證模式
如果未在 Database Engine 安裝期間啟用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 驗證，請在裝載 SSISDB 目錄的 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體上啟用 SQL Server 驗證模式。 

停用 SQL Server 驗證時，不會封鎖執行套件。 不過，執行記錄無法寫入至 SSISDB 資料庫。

## <a name="EnableWorker"></a> 啟用擴增背景工作

您可以使用 [Scale Out Manager](integration-services-ssis-scale-out-manager.md) (可提供圖形化使用者介面) 或預存程序來啟用 Scale Out Worker。

若要使用預存程序來啟用 Scale Out Worker，請執行將 **WorkerAgentId** 作為參數的 `[catalog].[enable_worker_agent]` 預存程序。 

向 Scale Out Master 註冊 Scale Out Worker 之後，從 SSISDB 的 `[catalog].[worker_agents]` 檢視中取得 **WorkerAgentId** 值。 啟動 Scale Out Master 和 Worker 服務之後，註冊需要數分鐘的時間。

#### <a name="example"></a>範例
下列範例會在 `computerA` 上啟用 Scale Out Worker。

```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName  --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    computerA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="next-steps"></a>後續步驟
-   [執行 Integration Services (SSIS) Scale Out 中的套件](run-packages-in-integration-services-ssis-scale-out.md).
