---
title: "逐步解說：設定 Integration Services 相應放大 | Microsoft Docs"
ms.custom: ""
ms.date: "01/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cabb78a2-f234-46c3-842d-53aa2df8dfb3
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# 逐步解說：設定 Integration Services 相應放大

您可以完成下列工作來設定 [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] 相應放大。 

> [!NOTE] 如果您要在一部電腦上安裝相應放大，建議您同時安裝相應放大主機和相應放大背景工作功能。 當您同時安裝這些功能時，會自動產生端點，以連接至相應放大主機。 

* [安裝相應放大主機](#InstallMaster)

* [安裝相應放大背景工作](#InstallWorker)

* [安裝相應放大背景工作用戶端憑證](#InstallCert)

* [開啟防火牆通訊埠](#Firewall)

* [啟動 SQL Server 相應放大主機和背景工作服務](#Start)

* [啟用相應放大主機](#EnableMaster)

* [啟用 SQL Server 驗證模式](#EnableAuth)

* [啟用相應放大背景工作](#EnableWorker)

## <a name="a-nameinstallmastera-install-scale-out-master"></a><a name="InstallMaster"></a> 安裝相應放大主機

若要啟用相應放大主機功能，您必須在設定 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 時安裝 Database Engine Services、[!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] 和其相應放大主機功能。 

如需設定 Database Engine Services 和 [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] 的相關資訊，請參閱[安裝 SQL Server Database Engine](../database-engine/install-windows/install-sql-server-database-engine.md) 和[安裝 Integration Services](../integration-services/install-windows/install-integration-services.md)。
> [!NOTE]
> 在 Database Engine 安裝期間，於 [資料庫引擎組態] 頁面上，針對 [驗證模式] 選取 [混合模式]。 

**若要安裝相應放大主機功能，請使用 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 安裝精靈或命令提示字元。**

- [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 安裝精靈的步驟
  1.  在 [特徵選取] 頁面上，選取列在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 下方的 [相應放大主機]。   
  ![特徵選取主機](../integration-services/media/feature-select-master.PNG)
  
  2.  在 [伺服器組態] 頁面上，選取要執行 [SQL Server Integration Services 相應放大主機服務] 的帳戶，然後選取 [啟動類型]。  
  ![伺服器組態](../integration-services/media/server-config.PNG)
  3.  在 [Integration Services 相應放大主機組態] 頁面上，指定相應放大主機用來與相應放大背景工作通訊的通訊埠編號。 預設通訊埠編號是 8391。  
  ![Master Config](../integration-services/media/master-config.PNG "Master Config")
  4.  執行下列其中一項，以指定用來保護相應放大主機與相應放大背景工作間之通訊的 SSL 憑證。
    * 按一下 [建立新的 SSL 憑證]，讓安裝程序建立預設自我簽署 SSL 憑證。 預設憑證會安裝到 [受信任的根憑證授權單位] 的 [本機電腦] 下方。
    * 按一下 [Use an existing SSL certificate (使用現有的 SSL 憑證)]，然後按一下 [瀏覽]，以選取本機電腦上的現有 SSL 憑證。 憑證的指紋會出現在文字方塊中。 按一下 [瀏覽] 會顯示在 [受信任的根憑證授權單位] 的 [本機電腦] 中所儲存的憑證。 您選取的憑證必須儲存在這裡。       
![Master Config 2](../integration-services/media/master-config-2.PNG "Master Config 2")
  5.  完成 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 安裝精靈。
- 命令提示字元的步驟

    請遵循[從命令提示字元安裝 SQL Server](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) 中的指示進行。 執行下列動作，以設定相應放大主機相關參數。
  1.  將 IS_Master 新增至 /FEATURES 參數
  2.  使用下列參數來設定相應放大主機：/ISMASTERSVCACCOUNT、/ISMASTERSVCPASSWORD、/ISMASTERSVCSTARTUPTYPE、/ISMASTERSVCPORT、/ISMASTERSVCTHUMBPRINT (選擇性)。
  
## <a name="a-nameinstallworkera-install-scale-out-worker"></a><a name="InstallWorker"></a> 安裝相應放大背景工作
 
若要啟用相應放大背景工作功能，您必須在 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 安裝時安裝 [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] 和其相應放大背景工作功能。

**若要安裝相應放大背景工作功能，請使用 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 安裝精靈或命令提示字元。**

- [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 安裝精靈的步驟
  1.  在 [特徵選取] 頁面上，選取列在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 下方的 [相應放大背景工作]。   
  ![特徵選取背景工作](../integration-services/media/feature-select-worker.PNG)
  2. 在 [伺服器組態] 頁面上，選取要執行 [SQL Server Integration Services 相應放大背景工作服務] 的帳戶，然後選取 [啟動類型]。    
  ![Server Config 2](../integration-services/media/server-config-2.PNG "Server Config 2")
  3. 在 [Integration Services 相應放大背景工作組態] 頁面上，指定連接至相應放大主機的端點。 
    - 針對 **One-box** 環境，同時安裝相應放大主機和相應放大背景工作時，即會自動產生端點。 
    - 針對**多部電腦**環境，端點包含已安裝相應放大主機之電腦的名稱或 IP，以及相應放大主機安裝期間所指定的通訊埠編號。    
   ![Worker Config 1](../integration-services/media/worker-config-1.PNG "Worker Config 1")
    
  4. 針對**多部電腦**環境，指定用來驗證相應放大主機的用戶端 SSL 憑證。 針對 **One-box** 環境，不需要指定用戶端 SSL 憑證。 
  
     > [!NOTE] 自我簽署相應放大主機所使用的 SSL 憑證時，需要在具有相應放大背景工作的電腦上安裝對應的用戶端 SSL 憑證。 如果您在 [Integration Services 相應放大背景工作組態] 頁面上提供用戶端 SSL 憑證的檔案路徑，則會自動予以安裝；否則，稍後您必須手動安裝憑證。 
     
     按一下 [瀏覽] 找出憑證檔案 (*.cer)。 若要使用預設 SSL 憑證，請選取位於已安裝相應放大主機之電腦的 \<磁碟機\>:\Program Files\Microsoft SQL Server\140\DTS\Binn 下方的 SSISScaleOutMaster.cer 檔案。   
   ![Worker Config 2](../integration-services/media/worker-config-2.PNG "Worker Config 2")
  5. 完成 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 安裝精靈。
- 命令提示字元的步驟

    請遵循[從命令提示字元安裝 SQL Server](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) 中的指示進行。 執行下列動作，以設定相應放大背景工作相關參數。
    1.  將 IS_Worker 新增至 /FEATURES 參數
    2. 使用下列參數來設定相應放大背景工作：/ISWORKERSVCACCOUNT、/ISWORKERSVCPASSWORD、/ISWORKERSVCSTARTUPTYPE、/ISWORKERSVCMASTER (選擇性)、/ISWORKERSVCCERT (選擇性)。

 
## <a name="a-nameinstallcerta-install-scale-out-worker-client-certificate"></a><a name="InstallCert"><a/> 安裝相應放大背景工作用戶端憑證

在安裝相應放大背景工作期間，將會在電腦上自動建立和安裝背景工作憑證。 同時，會在 \<磁碟機\>:\Program Files\Microsoft SQL Server\140\DTS\Binn 下方安裝對應的用戶端憑證 SSISScaleOutWorker.cer。 若要讓相應放大主機驗證相應放大背景工作，您必須將此用戶端憑證新增至具有相應放大主機之本機電腦的根存放區。
  
若要將用戶端憑證新增至根存放區，請連按兩下 .cer 檔案，然後按一下 [憑證] 對話方塊中的 [安裝憑證]。 即會顯示 [憑證匯入精靈]。  

## <a name="a-namefirewalla-open-firewall-port"></a><a name="Firewall"><a/> 開啟防火牆通訊埠

在相應放大主機電腦上使用 Windows 防火牆，以開啟在相應放大主機安裝期間所指定的通訊埠。
    
## <a name="a-namestarta-start-sql-server-scale-out-master-and-worker-services"></a><a name="Start"></a> 啟動 SQL Server 相應放大主機和背景工作服務

如果在上述的安裝期間未將服務的啟動類型設定為自動，請啟動服務︰SQL Server Integration Services 相應放大主機 14.0 (SSISScaleOutMaster140) 和 SQL Server Integration Services 相應放大背景工作 14.0 (SSISScaleOutWorker140)。 

> [!NOTE]
>在您開啟防火牆通訊埠之後，您需要重新啟動相應放大背景工作服務。
   
## <a name="a-nameenablemastera-enable-scale-out-master"></a><a name="EnableMaster"></a> 啟用相應放大主機

在 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../includes/ssmanstudio-md.md)] 中建立 SSISDB 目錄時，請按一下 [建立目錄] 對話方塊中的 [啟用此伺服器作為 SSIS 相應放大主機]。

## <a name="a-nameenableautha-enable-sql-server-authentication-mode"></a><a name="EnableAuth"></a> 啟用 SQL Server 驗證模式
如果未在 Database Engine 安裝期間啟用 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 驗證，請在主控 SSISDB 目錄的 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 執行個體上啟用 SQL Server 驗證模式。 

停用 SQL Server 驗證時，不會封鎖執行套件。 不過，執行記錄將無法寫入 SSISDB。

## <a name="a-nameenableworkera-enable-scale-out-worker"></a><a name="EnableWorker"></a> 啟用相應放大背景工作
若要啟用相應放大背景工作，請執行將 **WorkerAgentId** 作為參數的 *[catalog].[enable_worker_agent]* 預存程序。 

向相應放大主機註冊相應放大背景工作之後，您會從 SSISDB 的 *[catalog].[worker_agents]* 資料庫檢視中取得 **WorkerAgentId** 值。 啟動相應放大主機和背景工作服務之後，註冊需要數分鐘的時間。

### <a name="example"></a>範例
這個範例會在 MachineA 上啟用相應放大背景工作。
```tsql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```
## <a name="next-steps"></a>後續步驟
已完成相應放大功能設定。 您現在可以在相應放大中執行套件。 如需詳細資訊，請參閱[在 Integration Services (SSIS) 相應放大中執行套件](../integration-services/run-packages-in-integration-services-ssis-scale-out.md)。

