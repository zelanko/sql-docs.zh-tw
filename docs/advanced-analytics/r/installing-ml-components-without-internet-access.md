---
title: "安裝在機器學習 Components without Internet Access |Microsoft 文件"
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 30
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7307104b9ad5df2bb8f034525cc82847d21a14bf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="installing-machine-learning-components-without-internet-access"></a>安裝在機器學習 Components without Internet Access

因為 R，並將 Python 元件隨附 SQL Server 2016 或 SQL Server 2017 的開放原始碼，Microsoft 不會依預設安裝 R 或 Python 的元件。

相反地，我們會提供相關的安裝程式，並為了方便起見，Microsoft 下載中心和其他受信任的站台上建立封裝。 您必須同意將適當的授權，然後 SQL Server 安裝程式時，會為您安裝 R 或 Python 的元件。

本主題提供的下載位置，安裝程式和離線安裝程式程序的概觀。

## <a name="installation-process"></a>安裝處理

一般而言，用於 SQL Server 2016 和 SQL Server 2017 機器元件的安裝程式需要網際網路連線。 SQL Server 安裝程式執行時，如果您已選取的任何機器 learnig 選項，安裝程式會檢查 Python 或 R 安裝程式，以及任何其他必要元件。 如果沒有網際網路連線，SQL Server 會為您安裝它們。

> [!IMPORTANT]
> 在沒有網際網路存取伺服器上，您必須下載額外的安裝程式，再繼續安裝。

最小值，您必須下載的 R 或 Python 的安裝程式支援的版本，或您要安裝的 SQL Server 的組建編號。

根據您的伺服器組態，您可能需要額外的元件，例如.NET Core。  請參閱[其他元件](#bkmk_OtherComponents)如需詳細資訊。

您已下載安裝程式之後，您使用它們時做為 SQL Server 安裝程式的一部分安裝功能。

### <a name="step-1-obtain-additional-installers"></a>步驟 1： 取得額外的安裝程式

如**R**在 SQL Server 2016 和 SQL Server 2017，您必須取得兩個不同的安裝程式。 SQL Server 安裝精靈會確定它們已依正確順序安裝。

+ 安裝程式與**SRO**名稱中提供的開放原始碼的元件。
+ 與 Insallers **SRS**名稱中包含由 Microsoft，包括用於資料庫整合提供的元件。


如**Python**在 SQL Server 2017，下載單一封包檔，以及任何必要條件。


1. 在可存取網際網路的電腦上，從 [Microsoft 下載中心網站](#installerlocs)下載安裝程式，並儲存安裝程式而非執行安裝程式。
2. 將安裝程式 (CAB) 檔案複製到您要在其中安裝機器學習服務元件的電腦。
3. 目前，安裝精靈正在安裝英文版的預設值。 若要安裝使用不同的語言，修改這裡所述的安裝程式檔案名稱：[針對不同的語言地區設定所需修改](#modslocales)。
4. 下載任何額外的元件所需的資源，例如 MPI 或.NET 核心。
5. （選擇性） 您可以下載已封存的來源元件的程式碼的開放原始碼，但這並不是必要的 SQL Server 安裝程式，您可以在任何時間完成。 如需詳細資訊，請參閱[R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。


> [!NOTE]
> 請務必取得符合您要安裝之 SQL Server 版本的檔案。
> 
> SQL Server 2017 CTP 2.0 中，會提供對 Python 的支援。 舊版本中，包括 SQL Server 2016 中，不支援 Python。

SQL Server 2016 中的 R 服務的離線安裝程序的逐步解說，我們建議的文章[SQL Server 客戶諮詢團隊](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。 它也涵蓋修補和匯集安裝案例。


### <a name="step-2-run-offline-setup-using-the-sql-server-setup-wizard"></a>步驟 2： 執行離線安裝程式使用 SQL Server 安裝精靈

1. 執行 SQL Server 安裝精靈。
2. 當安裝精靈會顯示 授權 頁面上時，按一下 **接受**。
3. 對話方塊隨即開啟，提示您輸入**安裝路徑**的所需的封裝。
4. 按一下**瀏覽**找出包含您之前複製的安裝程式檔案的資料夾。
5. 如果找到正確的檔案，您可以按一下 [下一步] 來指出元件可用。
10. 完成 SQL Server 安裝精靈。
11. 執行必要的後續安裝步驟，以確定服務已啟用。

## <a name="installerlocs"></a>下載

版本  |下載連結  
---------|---------
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)
**SQL Server 2016 CU 1**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 CU 2**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**SQL Server 2016 CU 3**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)  |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 GDR**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**SQL Server 2017 CTP 1**     |
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**SQL Server 2017 CTP 1.1** |
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)
**SQL Server 2017 CTP 1.4** |
Microsoft R Open     |[SRO_xxxx_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)
Microsoft R Server     |[SRS_xxx.xxx_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)
**SQL Server 2017 CTP 2.0** |
Microsoft R Open     |[SRO_3.3.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842800)
Microsoft R Server     |[SRS_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842799)
開啟 Microsoft Python     |[SPO_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842828)
Microsoft Python 伺服器    |[SPS_9.1.0.0__1033.cab](https://go.microsoft.com/fwlink/?LinkId=842848)

如果您想要檢視 Microsoft 的原始程式碼，它是可供下載的封存.tar 格式：[下載 R Server 安裝程式](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#download)

### <a name = "bkmk_OtherComponents"></a>其他必要條件

根據您的環境，您可能需要針對下列必要條件製作安裝程式的本機複本。

元件  |版本
---------|---------
[Microsoft AS OLE DB Provider for SQL Server 2016](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25
[Microsoft Visual C++ 2013 可轉散發套件](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0
[Microsoft Visual C++ 2015 可轉散發套件](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0


## <a name="modslocales"></a>安裝針對不同語言的地區設定

如果您將 .cab 檔案當成 SQL Server 安裝程式的一部分下載到能存取網際網路的電腦上，安裝精靈會偵測本機語言並自動變更安裝程式的語言。

不過，如果您要將當地語系化版本的 SQL Server 安裝到無法存取網際網路的電腦上，並將 R 安裝程式下載到本機共用時，您必須手動編輯已下載檔案的名稱並插入您要安裝語言的正確語言識別項。

例如，如果您要安裝日文版的 SQL Server，您應該將檔案名稱從 SRS_8.0.3.0_**1033**.cab 變更為 SRS_8.0.3.0_**1041**.cab。


## <a name="slipstream-upgrades"></a>匯集升級

匯集安裝程式是指將補充程式或更新套用至失敗的執行個體安裝，以修正現有問題的功能。 這個方法的優點是在您執行安裝程式的同時更新 SQL Server，以避免稍後分別重新啟動。

+ 如果伺服器無法存取網際網路，您必須在更新程序開始「之前」下載 SQL Server 安裝程式，然後下載對應的 R 元件安裝程式版本。  根據預設，使用 SQL Server 不包含的 R 元件。

+ 如果您是*加入*這些元件*現有*安裝中，使用 SQL Server 安裝程式的更新的版本，然後對應更新版本的其他元件。 當您指定 R 功能是要安裝時，安裝程式會尋找符合的機器學習服務元件的安裝程式的版本。

## <a name="command-line-arguments-for-setup"></a>安裝程式命令列引數

在執行自動的安裝時，您必須提供下列的命令列引數。 請注意您不需要設定任何其他的旗標，以安裝其他所需的元件。 預設會以無訊息方式安裝必要元件，例如.NET core。

**安裝程式的位置**

- `/UPDATESOURCE`若要指定包含 SQL Server 更新的安裝程式的本機檔案的位置
- `/MRCACHEDIRECTORY`若要指定包含 R 元件封包檔的資料夾

**SQL Server 2016 中的 R 元件**

- `/ADVANCEDANALYTICS`若要取得引擎支援的外部指令碼
- `/IACCEPTROPENLICENSETERMS="True"`若要接受授權合約的個別 R

**在 SQL Server SQL Server 2017 的 R 元件**

- `/ADVANCEDANALYTICS`若要取得引擎支援的外部指令碼
- `/SQL_INST_MR`若要使用 R
- `/IACCEPTROPENLICENSETERMS="True"`若要接受授權合約的個別 R

**在 SQL Server 2017 Python 元件**

- `/ADVANCEDANALYTICS`若要取得引擎支援的外部指令碼
- `/SQL_INST_MPY`若要使用 Python
- `/IACCEPTPYTHONLICENSETERMS="True"`若要接受授權合約的個別 R

> [!TIP]
> R 服務支援小組的這篇文章會示範如何在 SQL Server 2016 執行自動的安裝或升級 R 服務：[沒有網際網路存取的電腦上部署 R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。

## <a name="see-also"></a>另請參閱

[安裝 Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)


