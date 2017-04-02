---
title: "設定 Windows 防火牆以允許 Analysis Services 存取 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "通訊埠 [Analysis Services]"
  - "Windows 防火牆 [Analysis Services]"
  - "防火牆系統 [Analysis Services]"
ms.assetid: 7673acc5-75f0-4703-9ce2-87425ea39d49
caps.latest.revision: 47
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 47
---
# 設定 Windows 防火牆以允許 Analysis Services 存取
  讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 在網路上可供使用的第一個必要步驟為判斷您是否需要在防火牆中解除封鎖通訊埠。 大部分安裝都要求您至少建立一個傳入防火牆規則來允許連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
 防火牆組態需求視 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 安裝方式而異：  
  
-   當您安裝預設執行個體或建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 容錯移轉叢集時，開啟 TCP 通訊埠 2383。  
  
-   安裝具名執行個體時，開啟 TCP 通訊埠 2382。 具名執行個體使用動態通訊埠指派。 作為 Analysis Services 的探索服務，SQL Server Browser 服務會接聽 TCP 通訊埠 2382，並將連接要求重新導向至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 目前使用的連接埠。  
  
-   以 SharePoint 模式安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 時，開啟 TCP 通訊埠 2382 以支援 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013。 在 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體是在 SharePoint 外部。 對於具名 '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]' 執行個體的傳入要求是透過網路連接源自 SharePoint Web 應用程式，因此需要開啟連接埠。 如同其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 具名執行個體，為在 TCP 2382 的 SQL Server Browser 服務建立輸入規則，以允許存取 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]。  
  
-   如果是 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010，請勿在 Windows 防火牆中開啟連接埠。 做為 SharePoint 增益集，此服務會使用為 SharePoint 設定的通訊埠，而且只對載入和查詢 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料模型的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 執行個體建立本機連接。  
  
-   如果是在 Windows Azure 虛擬機器上執行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，請使用設定伺服器存取的其他指示。 請參閱 [Azure 虛擬機器中的 SQL Server Business Intelligence](http://msdn.microsoft.com/library/windowsazure/jj992719.aspx)。  
  
 雖然預設的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會接聽 TCP 通訊埠 2383，但是您可以用 \<伺服器名稱>:\<連接埠號碼> 格式連接至伺服器，設定讓伺服器接聽不同的固定連接埠。  
  
 只有一個 TCP 通訊埠可供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體使用。 在擁有多網路卡或多個 IP 位址的電腦上，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會接聽一個指派給電腦之所有 IP 位址或別名位址的 TCP 通訊埠。 如果您有特定多通訊埠需求，請考慮設定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用 HTTP 存取。 如此一來，您就可以將多個 HTTP 端點設定在所選擇的通訊埠。 請參閱[設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md)。  
  
 本主題包含下列幾節：  
  
-   [檢查 Analysis Services 所使用的通訊埠和防火牆設定](#bkmk_checkport)  
  
-   [為 Analysis Services 的預設執行個體設定 Windows 防火牆](#bkmk_default)  
  
-   [為 Analysis Services 的具名執行個體設定 Windows 防火牆存取](#bkmk_named)  
  
-   [Analysis Services 叢集的通訊埠組態](#bkmk_cluster)  
  
-   [Power Pivot for SharePoint 的通訊埠組態](#bkmk_powerpivot)  
  
-   [針對 Analysis Services 的預設或具名執行個體使用固定通訊埠](#bkmk_fixed)  
  
 如需預設 Windows 防火牆設定的詳細資訊以及影響 Database Engine、Analysis Services、Reporting Services 和 Integration Services 之 TCP 通訊埠的描述，請參閱[設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
##  <a name="bkmk_checkport"></a> 檢查 Analysis Services 所使用的通訊埠和防火牆設定  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援的 Microsoft Windows 作業系統中，Windows 防火牆預設為開啟，並且封鎖了遠端連線。 您必須手動在防火牆中開啟通訊埠，允許傳入要求至 Analysis Services。 SQL Server 安裝程式不會為您執行此步驟。  
  
 您可以在 msmdsrv.ini 檔和 SQL Server Management Studio 之 Analysis Services 執行個體的 [一般屬性] 頁面中指定通訊埠設定。 如果 [連接埠] 設定為正整數，表示服務將接聽固定連接埠。 如果 [連接埠] 設定為 0，表示服務將接聽連接埠 2383 (Analysis Services 執行個體為預設執行個體) 或動態指派的連接埠 (Analysis Services 執行個體為具名執行個體)。  
  
 只有具名執行個體會使用動態通訊埠指派。 **MSOLAP$InstanceName** 服務會在啟動時決定要使用的連接埠。 您可以執行下列步驟，決定要由具名執行個體使用的實際通訊埠編號：  
  
-   啟動 [工作管理員]，然後按一下 [服務] 以取得 **MSOLAP$InstanceName** 的 PID。  
  
-   從命令列執行 **netstat –ao –p TCP**，查看該 PID 使用的 TCP 通訊埠資訊。  
  
-   使用 SQL Server Management Studio 並使用 \<IP 位址>:\<連接埠號碼> 格式連接到 Analysis Services 伺服器，確認該連接埠正確無誤。  
  
 雖然應用程式將接聽特定通訊埠，但是只要防火牆封鎖存取權限，連接作業就不會成功。 您必須解除封鎖 msmdsrv.exe 或此程式在防火牆中接聽之固定通訊埠的存取權限，才能連接到具名 Analysis Services 執行個體。 本主題的其他章節將指示您如何解除封鎖存取權限。  
  
 若要確認是否已針對 Analysis Services 定義防火牆設定，請使用 [控制台] 中的 [具有進階安全性的 Windows 防火牆]。 [監視] 節點下的 [防火牆] 頁面會顯示針對本機伺服器定義的完整規則清單。  
  
 請注意，對於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，必須手動定義所有防火牆規則。 雖然 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 SQL Server Browser 會保留連接埠 2382 和 2383，但是 SQL Server 安裝程式與所有組態工具都不會定義可允許存取連接埠或程式可執行檔的防火牆規則。  
  
##  <a name="bkmk_default"></a> 為 Analysis Services 的預設執行個體設定 Windows 防火牆  
 預設的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會接聽 TCP 通訊埠 2383。 如果您安裝了預設執行個體，並要使用此連接埠，只需要在 Windows 防火牆中，解除封鎖對 TCP 通訊埠 2383 的傳入存取，即可從遠端存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的預設執行個體。 如果您安裝了預設執行個體，但要將服務設定為接聽固定連接埠，請參閱本主題中的[針對 Analysis Services 的預設或具名執行個體使用固定連接埠](#bkmk_fixed)。  
  
 若要確認服務是否做為預設執行個體 (MSSQLServerOLAPService) 在運作，請檢查 [SQL Server 組態管理員] 中的服務名稱。 Analysis Services 的預設執行個體一律會顯示為 **SQL Server Analysis Services (MSSQLSERVER)**。  
  
> [!NOTE]  
>  不同的 Windows 作業系統可提供替代工具來設定 Windows 防火牆。 這些工具大部分都能讓您選擇要開啟指定通訊埠還是程式可執行檔。 除非有指定程式可執行檔的需求，否則建議您指定通訊埠。  
  
 指定輸入規則時所使用的命名慣例，必須方便您日後能夠輕易地找到規則 (例如 **SQL Server Analysis Services (TCP-in) 2383**)。  
  
#### 具有進階安全性的 Windows 防火牆  
  
1.  在 Windows 7 或 Windows Vista 的 [控制台] 中按一下 [系統及安全性]，然後選取 [Windows 防火牆]，再按一下 [進階設定]。 在 Windows Server 2008 或 2008 R2，開啟 [系統管理工具]，然後按一下 [具有進階安全性的 Windows 防火牆]。 在 Windows Server 2012 上，開啟 [應用程式] 頁面並輸入 **Windows Firewall**。  
  
2.  以滑鼠右鍵按一下 [輸入規則]，然後選取 [新增規則]。  
  
3.  在 [規則類型] 中按一下 [連接埠]，然後按一下 [下一步]。  
  
4.  在 [通訊協定及連接埠] 中選取 [TCP]，然後在 [特定本機連接埠] 中輸入 **2383**。  
  
5.  在 [執行動作] 中按一下 [允許連線]，然後按一下 [下一步]。  
  
6.  在 [設定檔] 中，清除不適用的所有網路位置，然後按一下 [下一步]。  
  
7.  在 [名稱] 中，輸入此規則的描述性名稱 (例如 **SQL Server Analysis Services (tcp-in) 2383**)，然後按一下 [完成]。  
  
8.  如果要確認有無啟用遠端連接，請在不同的電腦上開啟 SQL Server Management Studio 或 Excel，然後在 [伺服器名稱] 中指定伺服器的網路名稱，以連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
    > [!NOTE]  
    >  您必須先授與其他使用者此伺服器的權限，才可存取此伺服器。 如需詳細資訊，請參閱[物件和作業的存取權授權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)。  
  
#### Netsh AdvFirewall 語法  
  
-   下列命令會建立輸入規則，允許內送要求使用 TCP 通訊埠 2383。  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services inbound on TCP 2383" dir=in action=allow protocol=TCP localport=2383 profile=domain  
    ```  
  
##  <a name="bkmk_named"></a> 為 Analysis Services 的具名執行個體設定 Windows 防火牆存取  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的具名執行個體可以在固定通訊埠上接聽，也可在動態指派的通訊埠上接聽 (若為後者，SQL Server Browser 服務會在連接時提供最新服務連接資訊)。  
  
 SQL Server Browser 服務會接聽 TCP 通訊埠 2382。 不使用 UDP。 TCP 是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 唯一使用的傳輸通訊協定。  
  
 選擇下列其中一種方法，以啟用 Analysis Services 之具名執行個體的遠端存取：  
  
-   使用動態通訊埠指派與 SQL Server Browser 服務。 在 Windows 防火牆中解除封鎖 SQL Server Browser 服務所使用的通訊埠。 以下列格式連接至伺服器：\<伺服器名稱>\\<執行個體名稱\>。  
  
-   使用固定通訊埠與 SQL Server Browser 服務。 此方法除會接聽固定連接埠之外，其他皆與動態連接埠指派方法相同，也可使用下列格式連接：\<伺服器名稱>\\<執行個體名稱\>。 在此情況下，SQL Server Browser 服務會提供名稱解析給接聽固定通訊埠的 Analysis Services 執行個體。 如果要使用此方法，必須將伺服器設定為接聽固定通訊埠，並解除對該通訊埠存取的封鎖，以及解除對 SQL Server Browser 服務所用之通訊埠存取的封鎖。  
  
 SQL Server Browser 服務只可搭配具名執行個體使用，而不可與預設執行個體並用。 當您將 SQL Server 功能安裝成具名執行個體安裝時，即會自動安裝並啟用此服務。 如果您選擇的方法需要使用 SQL Server Browser 服務，請確認您的伺服器已啟用並啟動該服務。  
  
 如果您無法使用 SQL Server Browser 服務，您必須在連接字串中指派固定通訊埠，略過網域名稱解析。 在沒有 SQL Server Browser 服務的情況下，所有用戶端連接皆必須在連接字串中加入通訊埠編號 (例如 AW-SRV01:54321)。  
  
 **選項 1：使用動態通訊埠指派，並解除對 SQL Server Browser 服務存取的封鎖**  
  
 **MSOLAP$InstanceName** 會在此服務啟動之時，建立 Analysis Services 之具名執行個體的動態連接埠指派。 服務預設會宣告所找到的第一個可用通訊埠編號，而且每次重新啟動服務時，都會使用不同的通訊埠編號。  
  
 執行個體名稱解析是由 SQL Server Browser 服務處理。 如果要並用動態通訊埠指派與具名執行個體，必須解除對 SQL Server Browser 服務之 TCP 通訊埠 2382 的封鎖。  
  
> [!NOTE]  
>  SQL Server Browser 服務會分別在 UDP 通訊埠 1434 和 TCP 通訊埠 2382 接聽 Database Engine 和 Analysis Services。 即使您已經解除封鎖 UDP 通訊埠 1434 供 SQL Server Browser 服務使用，仍然必須解除封鎖 TCP 通訊埠 2382 供 Analysis Services 使用。  
  
#### 具有進階安全性的 Windows 防火牆  
  
1.  在 Windows 7 或 Windows Vista 的 [控制台] 中按一下 [系統及安全性]，然後選取 [Windows 防火牆]，再按一下 [進階設定]。 在 Windows Server 2008 或 2008 R2，開啟 [系統管理工具]，然後按一下 [具有進階安全性的 Windows 防火牆]。 在 Windows Server 2012 上，開啟 [應用程式] 頁面並輸入 **Windows Firewall**。  
  
2.  如果要解除對 SQL Server Browser 服務存取的封鎖，請以滑鼠右鍵按一下 [輸入規則]，然後選取 [新增規則]。  
  
3.  在 [規則類型] 中按一下 [連接埠]，然後按一下 [下一步]。  
  
4.  在 [通訊協定及連接埠] 中選取 [TCP]，然後在 [特定本機連接埠] 中輸入 **2382**。  
  
5.  在 [執行動作] 中按一下 [允許連線]，然後按一下 [下一步]。  
  
6.  在 [設定檔] 中，清除不適用的所有網路位置，然後按一下 [下一步]。  
  
7.  在 [名稱] 中輸入此規則的描述性名稱 (例如 **SQL Server Browser Service (tcp-in) 2382**)，然後按一下 [完成]。  
  
8.  如果要確認有無啟用遠端連接，請在不同的電腦上開啟 SQL Server Management Studio 或 Excel，然後使用 \<伺服器名稱>\\<執行個體名稱\> 格式，指定伺服器的網路名稱與執行個體名稱，以連接至 Analysis Services。 例如，在名稱為 **AW-SRV01** 且具有 **Finance** 具名執行個體的伺服器上，伺服器名稱為 **AW-SRV01\Finance**。  
  
 **選項 2：針對具名執行個體使用固定通訊埠**  
  
 或者，您也可以指派固定通訊埠，然後解除封鎖該通訊埠的存取權限。 此方法相較於允許存取程式可執行檔，可以提供更好的稽核功能。 因此在存取任何 Analysis Services 執行個體時，建議您使用固定通訊埠的方法。  
  
 若要指派固定連接埠，請遵循本主題[針對 Analysis Services 的預設或具名執行個體使用固定連接埠](#bkmk_fixed)中的指示操作，再回到本節解除封鎖連接埠。  
  
#### 具有進階安全性的 Windows 防火牆  
  
1.  在 Windows 7 或 Windows Vista 的 [控制台] 中按一下 [系統及安全性]，然後選取 [Windows 防火牆]，再按一下 [進階設定]。 在 Windows Server 2008 或 2008 R2，開啟 [系統管理工具]，然後按一下 [具有進階安全性的 Windows 防火牆]。 在 Windows Server 2012 上，開啟 [應用程式] 頁面並輸入 [Windows 防火牆]。  
  
2.  若要解除封鎖對 Analysis Services 的存取，請以滑鼠右鍵按一下 [輸入規則]，然後選取 [新增規則]。  
  
3.  在 [規則類型] 中按一下 [連接埠]，然後按一下 [下一步]。  
  
4.  在 [通訊協定及連接埠] 中選取 [TCP]，然後在 [特定本機連接埠] 中輸入固定連接埠號碼。  
  
5.  在 [執行動作] 中按一下 [允許連線]，然後按一下 [下一步]。  
  
6.  在 [設定檔] 中，清除不適用的所有網路位置，然後按一下 [下一步]。  
  
7.  在 [名稱] 中輸入此規則的描述性名稱 (例如 **連接埠 54321 的 SQL Server Analysis Services**)，然後按一下 [完成]。  
  
8.  若要確認有無啟用遠端連接，請在不同的電腦上開啟 SQL Server Management Studio 或 Excel，然後使用 \<伺服器名稱>:\<連接埠號碼> 格式，指定伺服器的網路名稱與連接埠號碼，以連接至 Analysis Services。  
  
#### Netsh AdvFirewall 語法  
  
-   下列命令所建立的輸入規則，可解除對 SQL Server Browser 服務所使用之 TCP 2382 的封鎖，以及解除您為 Analysis Services 執行個體所指定之固定通訊埠的封鎖。 您可以執行任一個命令允許對 Analysis Services 具名執行個體的存取。  
  
     在此範例命令中，通訊埠 54321 是固定通訊埠。 請務必以您系統所使用的實際通訊埠加以取代。  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services (tcp-in) on 54321" dir=in action=allow protocol=TCP localport=54321 profile=domain  
    ```  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Browser Services inbound on TCP 2382" dir=in action=allow protocol=TCP localport=2382 profile=domain  
    ```  
  
##  <a name="bkmk_fixed"></a> 針對 Analysis Services 的預設或具名執行個體使用固定通訊埠  
 本節說明如何將 Analysis Services 設定為接聽固定通訊埠。 如果將 Analysis Services 安裝成具名執行個體，一般會使用固定通訊埠；但如果是因為商務或安全性需要而必須使用非預設的通訊埠指派，也可使用此方法。  
  
 請注意，使用固定通訊埠時，由於必須將通訊埠編號附加至伺服器名稱，因此將變更預設執行個體的連接語法。 例如連接到 SQL Server Management Studio 中接聽通訊埠 54321 的本機預設 Analysis Services 執行個體時，必須在 Management Studio 的 [連接到伺服器] 對話方塊中輸入 localhost:54321 做為伺服器名稱。  
  
 如果您是使用具名執行個體，即可指派固定連接埠，而不必變更伺服器名稱的指定方式 (具體而言，您可以使用 \<servername\instancename> 連接到接聽固定連接埠的具名執行個體)。 SQL Server Browser 服務必須在執行中，才可解除對其所接聽之通訊埠的封鎖。 SQL Server Browser 服務會根據 \<servername\instancename> 重新導向至固定連接埠。 只要您開啟通訊埠供 SQL Server Browser 服務和接聽固定通訊埠的 Analysis Services 具名執行個體使用，SQL Server Browser 服務就會將連線解析為具名執行個體。  
  
1.  決定可供使用的 TCP/IP 通訊埠。  
  
     若要檢視您應該避免使用的保留與已註冊連接埠清單，請參閱 [Port Numbers (IANA)](http://go.microsoft.com/fwlink/?LinkID=198469) (連接埠號碼 (IANA))。 若要檢視系統已經使用的連接埠清單，請開啟命令提示字元視窗，然後輸入 **netstat –a –p TCP** 來顯示系統中已經開啟的 TCP 通訊埠清單。  
  
2.  一旦決定要使用的連接埠之後，請在 msmdsrv.ini 檔或是在 SQL Server Management Studio 之 Analysis Services 執行個體的 [一般屬性] 頁面中編輯 [連接埠] 組態設定以指定連接埠。  
  
3.  重新啟動服務。  
  
4.  設定 Windows 防火牆，解除封鎖您指定的 TCP 通訊埠。 如果您要讓具名執行個體使用固定通訊埠，請解除封鎖您指定的 TCP 通訊埠讓該執行個體使用，以及解除封鎖 TCP 通訊埠 2382 供 SQL Server Browser 服務使用。  
  
5.  以本機方式連接 (在 Management Studio 中)，然後從其他電腦上的用戶端應用程式以遠端方式連接，確認上述通訊埠是否已開啟。 若要使用 Management Studio，請以 \<伺服器名稱>:\<連接埠號碼> 格式指定伺服器名稱，連接到 Analysis Services 預設執行個體。 對於具名執行個體，請將伺服器名稱指定為 \<伺服器名稱>\\<執行個體名稱\>。  
  
##  <a name="bkmk_cluster"></a> Analysis Services 叢集的通訊埠組態  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 容錯移轉叢集一定會接聽 TCP 通訊埠 2383，不論您將它安裝為預設執行個體還是具名執行個體。 在 Windows 容錯移轉叢集上安裝時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不會使用動態連接埠指派。 請務必在叢集中執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的每個節點上開啟 TCP 2383。 如需叢集化 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的詳細資訊，請參閱 [How to Cluster SQL Server Analysis Services](http://go.microsoft.com/fwlink/p/?LinkId=396548) (如何將 SQL Server Analysis Services 叢集化)。  
  
##  <a name="bkmk_powerpivot"></a> Power Pivot for SharePoint 的通訊埠組態  
 根據使用的 SharePoint 版本，[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 的伺服器架構有本質上的不同。  
  
 **SharePoint 2013**  
  
 在 SharePoint 2013 中，Excel Services 會將 Power Pivot 資料模型的要求重新導向，隨後在 SharePoint 環境之外的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上載入。 連接遵循一般模式，也就是由本機電腦上的 Analysis Services 用戶端程式庫傳送連接要求給相同網路中的遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。  
  
 由於 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 一定會安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 當做具名執行個體，您應該採用 SQL Server Browser 服務與動態通訊埠指派。 如前所述，SQL Server Browser 服務會接聽 TCP 通訊埠 2382 傳送到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 具名執行個體的連接要求，並將要求重新導向至目前的通訊埠。  
  
 請注意，SharePoint 2013 中的 Excel Services 不支援固定通訊埠連接語法，因此請確定可以存取 SQL Server Browser 服務。  
  
 **SharePoint 2010**  
  
 如果您是使用 SharePoint 2010，就不必開啟 Windows 防火牆中的通訊埠。 SharePoint 會開啟它所需要的連接埠，而且增益集 (例如 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint) 會在 SharePoint 環境中運作。 在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 2010 安裝中，[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務會獨佔使用在相同電腦上一併安裝的本機 SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 服務執行個體。 其會使用本機連線 (而非網路連線) 存取本機 Analysis Services 引擎服務，而該服務會載入、查詢及處理 SharePoint 伺服器上的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料。 若要從用戶端應用程式要求 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料，這些要求會透過 SharePoint 安裝程式所開啟的連接埠來傳送 (具體而言，是定義輸入規則以允許存取 SharePoint – 80、SharePoint 管理中心 v4、SharePoint Web 服務和 SPUserCodeV4)。 由於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Web 服務是在 SharePoint 伺服陣列中運作，因此要遠端存取 SharePoint 伺服陣列中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料，使用 SharePoint 防火牆規則已經足夠。  
  
## 請參閱＜  
 [SQL Server Browser 服務 &#40;Database Engine 和 SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)   
 [啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](../../database-engine/configure-windows/start, stop, pause, resume, restart sql server services.md)   
 [設定用於 Database Engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
  