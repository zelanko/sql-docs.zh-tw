---
title: "安裝沒有網際網路存取的機器學習元件 |Microsoft 文件"
ms.custom: 
ms.date: 01/08/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 1c4a63077cf9801a6c83502f2fdea6f88c063227
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="installing-machine-learning-components-without-internet-access"></a>安裝沒有網際網路存取的機器學習服務元件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

因為 R，並將 Python 元件提供 SQL Server 2016 和 SQL Server 2017 的開放原始碼，Microsoft 不會依預設安裝 R 或 Python 的元件。 相反地，我們會提供相關的安裝程式，並為了方便起見，Microsoft 下載中心和其他受信任的站台上建立封裝。 您必須同意將適當的授權，然後 SQL Server 安裝程式會為您的 R 或 Python 的元件。

本主題提供的下載位置，安裝程式和離線安裝程式程序的概觀。

## <a name="overview-of-the-offline-installation-process"></a>離線安裝程序概觀

一般而言，用於 SQL Server 2016 和 SQL Server 2017 機器元件的安裝程式需要網際網路連線。 SQL Server 安裝程式執行時，如果已選取的機器學習選項，安裝程式會檢查 Python 或 R 安裝程式，以及任何其他必要元件。

+ **如果電腦有網際網路連線**

    SQL Server 找出並下載元件，並進行安裝期間安裝。 接受授權條款，分別為您安裝每個開放原始碼元件 （R 或 Python）。

+ **如果電腦沒有網際網路存取**

    您必須下載其他的安裝程式，再繼續安裝。 最小值，下載您要安裝的 SQL Server 版本支援的 R 或 Python 安裝程式。

    根據您的伺服器組態，您可能需要額外的元件。  請參閱[其他元件](#bkmk_OtherComponents)如需詳細資訊。

    您已下載安裝程式之後，您使用它們時做為 SQL Server 安裝程式的一部分安裝功能。

### <a name="step-1-obtain-additional-installers"></a>步驟 1： 取得額外的安裝程式

**R**

SQL Server 2016 和 SQL Server 2017 可支援的 R 語言。 兩個不同的安裝程式所需，開放原始碼和專屬的元件。 SQL Server 安裝精靈可確保它們會安裝在正確的順序。

+ 安裝程式與**SRO**名稱中提供的開放原始碼的元件。
+ 安裝程式與**SRS**名稱中包含由 Microsoft，包括用於資料庫整合提供的元件。

**Python**

Python 語言只支援 SQL Server 2017。 同樣地也有兩個不同的安裝程式，您必須下載。

+ 安裝程式與**SPO**名稱中適用於 Microsoft Python 開啟，並提供開放原始碼元件。
+ 安裝程式與**SPS**名稱中是與 Microsoft Python 伺服器，並包含 Microsoft，包括用於資料庫整合所提供的元件。

**如何下載**

1. 下載安裝程式從[Microsoft 下載中心網站](#installerlocs)至具有網際網路存取權，並且儲存安裝程式，而不會執行它的電腦。
2. 將安裝程式 (CAB) 檔案複製到您要安裝的機器學習服務元件的電腦。
3. 在 SQL Server 2016 中，安裝精靈會依預設安裝英文版。 使用不同的語言來安裝所需修改安裝程式檔案名稱，如下所述：[修改所需的不同語言的地區設定](#modslocales)。
    針對 SQL Server 2017，正確的語言會根據執行個體的地區設定識別。
4. 下載任何額外的元件所需的資源，例如 MPI 或.NET 核心。
5. （選擇性） 您可以下載已封存的來源元件的程式碼的開放原始碼，但這並不是必要的 SQL Server 安裝程式，您可以在任何時間完成。 如需詳細資訊，請參閱[R Server for Windows](https://docs.microsoft.com/r-server/install/r-server-install-windows)。

SQL Server 2016 中的 R 服務的離線安裝程序的逐步解說，我們建議的文章[SQL Server 客戶諮詢團隊](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。 文件包含螢幕擷取畫面，另外也涵蓋了修補和匯集安裝案例。

### <a name="step-2-run-offline-setup-using-the-sql-server-setup-wizard"></a>步驟 2： 執行離線安裝程式使用 SQL Server 安裝精靈

1. 執行 SQL Server 安裝精靈。
2. 當安裝精靈會顯示 授權 頁面上時，按一下 **接受**。
3. 對話方塊隨即開啟，提示您輸入**安裝路徑**的所需的封裝。
4. 按一下**瀏覽**找出包含您之前複製的安裝程式檔案的資料夾。
5. 如果找到正確的檔案，您可以按一下 [下一步] 來指出元件可用。
10. 完成 SQL Server 安裝精靈。
11. 執行必要的後續安裝步驟，以確定服務已啟用。

## <a name="installerlocs"></a>若要下載機器學習服務元件的位置

> [!NOTE]
> 請務必取得符合您要安裝的 SQL Server 版本的檔案。
> 
> 從 SQL Server 2017 CTP 2.0 提供的 Python 的支援。 舊版本中，包括 SQL Server 2016 中，不支援 Python。

+ [取得 SQL Server 2016 中的 R 元件](#bkmk_2016Installers)

+ [若要取得 SQL Server 2017 R 或 Python 元件](#bkmk_2017Installers)

### <a name="bkmk_2017Installers"></a>下載適用於 SQL Server 2017

版本  |下載連結  |
---------|---------|
**SQL Server 2017 CTP 1**     |
Microsoft R Open     |[SRO_3.3.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)
Microsoft R Server     |[SRS_9.0.0.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)
**SQL Server 2017 CTP 1.1** |
Microsoft R Open     |[SRO_3.3.2.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834568)
Microsoft R Server     |[SRS_9.0.1.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=834567)
**SQL Server 2017 CTP 1.4** |
Microsoft R Open     |[SRO_3.3.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842483)
Microsoft R Server     |[SRS_9.0.2.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842482)
**SQL Server 2017 CTP 2.0** |
Microsoft R Open     |[SRO_3.3.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842800)
Microsoft R Server     |[SRS_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842799)
開啟 Microsoft Python     |[SPO_9.1.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=842828)
Microsoft Python Server    |[SPS_9.1.0.0__1033.cab](https://go.microsoft.com/fwlink/?LinkId=842848)
**SQL Server 2017 RC1** |
Microsoft R Open     |[SRO_3.3.3.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851503)|
Microsoft R Server     |[SRS_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851498)|
開啟 Microsoft Python     |[SPO_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851499)|
Microsoft Python Server    |[SPS_9.2.0.22_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851504)|
**SQL Server 2017 RC 2** |
Microsoft R Open     |[SRO_3.3.3.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851493)|
Microsoft R Server     |[SRS_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851505)|
開啟 Microsoft Python     |[SPO_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851506)|
Microsoft Python Server    |[SPS_9.2.0.23_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851497)|
**SQL Server 2017 RTM** |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
開啟 Microsoft Python     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |
**SQL Server 2017 CU1** |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
開啟 Microsoft Python     |不是變更，使用上一個 |
Microsoft Python Server    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) |
**SQL Server 2017 CU2** |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server      |不是變更，使用上一個|
開啟 Microsoft Python     |不是變更，使用上一個|
Microsoft Python Server    |不是變更，使用上一個|
**SQL Server 2017 CU3** |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
開啟 Microsoft Python     |不是變更，使用上一個|
Microsoft Python Server    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)|

### <a name="bkmk_2016Installers"></a>下載適用於 SQL Server 2016

> [!IMPORTANT]
> 
> 離線安裝 SQL Server 2016 SP1 CU4 或 SP1 CU5 時, 下載 SRO_3.2.2.16000_1033.cab。 如果在安裝程式 對話方塊中所示，您可以下載從 FWLINK 831785 的 SRO_3.2.2.13000_1033.cab，檔案重新命名為 SRO_3.2.2.16000_1033.cab 之前安裝累計更新。

版本  |下載連結  |
---------|---------|
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
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server     | 不是變更，使用上一個 |
**SQL Server 2016 CU 4**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU 5**     |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server     |不是變更，使用上一個|
**SQL Server 2016 CU 6**     |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server     |[SRS_8.0.3.14000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850316)  |
**SQL Server 2016 CU 7**     |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server     |不是變更，使用上一個 |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 CU1**     |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server     |不是變更，使用上一個|
**SQL Server 2016 SP 1 CU2**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP 1 CU3**     |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server     |不是變更，使用上一個|
**SQL Server 2016 SP 1 CU4 和 GDR**     |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP 1 CU5**     |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server    |不是變更，使用上一個 |

如果您想要檢視 Microsoft 的原始程式碼，它是可供下載的封存.tar 格式：[下載 R Server 安裝程式](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

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

如果您下載。具有網際網路存取，安裝精靈的電腦上的封包檔做為 SQL Server 安裝程式的一部分會偵測本機語言，並會自動變更的安裝程式語言。

不過，根據您的 SQL Server 版本，您可能需要採取額外步驟來存取網際網路的電腦上安裝當地語系化的 R 元件。

+ **適用於 SQL Server 2016**

   R 安裝程式下載到本機共用之後，您可能需要以手動方式編輯下載的檔案，將您要安裝的語言的正確的語言識別項的名稱。

    例如，若要安裝日文版的 SQL Server，您會變更檔案的名稱從 SRS_8.0.3.0_**1033年**SRS_8.0.3.0_ 的.cab**1041年**.cab。

    > [!IMPORTANT]
    > 此問題適用於僅為早期版本，而且已在較新版本中修正。
    > **只有當安裝程式傳回的訊息，它無法安裝正確的語言時，才能使用這個因應措施。**

+ **For SQL Server 2017**

    下載。R 或 Python 元件的封包檔。
    
    語言會偵測到依據伺服器地區設定。 正確的地區設定會自動安裝使用下載。封包檔。

## <a name="slipstream-upgrades"></a>匯集升級

匯集安裝程式是指將補充程式或更新套用至失敗的執行個體安裝，以修正現有問題的功能。 這個方法的優點是在您執行安裝程式的同時更新 SQL Server，以避免稍後分別重新啟動。

+ 如果伺服器無法存取網際網路，您必須在更新程序開始「之前」下載 SQL Server 安裝程式，然後下載對應的 R 元件安裝程式版本。  根據預設，使用 SQL Server 不包含的 R 元件。

+ 如果您是*加入*這些元件*現有*安裝中，使用 SQL Server 安裝程式的更新的版本，然後對應更新版本的其他元件。 當您指定 R 功能是要安裝時，安裝程式會尋找符合的機器學習服務元件的安裝程式的版本。

## <a name="command-line-arguments-for-specifying-component-locations"></a>命令列引數指定元件的位置

當從命令列執行離線安裝程式，您必須提供下列的命令列引數來指定您事先下載元件的位置。 不過，您不需要設定任何其他的旗標，以安裝其他必要的元件。預設會以無訊息方式安裝必要元件，例如.NET core。

**安裝程式的位置**

- `/UPDATESOURCE`若要指定包含 SQL Server 更新的安裝程式的本機檔案的位置
- `/MRCACHEDIRECTORY`若要指定包含 R 元件封包檔的資料夾
- `/MPYCACHEDIRECTORY`若要指定包含 Python 元件封包檔的資料夾

**SQL Server 2016 中的 R 元件**

- `/ADVANCEDANALYTICS`若要取得引擎支援的外部指令碼
- `/IACCEPTROPENLICENSETERMS="True"`若要接受授權合約的個別 R

**在 SQL Server 2017 的 R 元件**

- `/ADVANCEDANALYTICS`若要取得引擎支援的外部指令碼
- `/SQL_INST_MR`若要使用 R
- `/IACCEPTROPENLICENSETERMS="True"`若要接受授權合約的個別 R

**在 SQL Server 2017 Python 元件**

- `/ADVANCEDANALYTICS`若要取得引擎支援的外部指令碼
- `/SQL_INST_MPY`若要使用 Python
- `/IACCEPTPYTHONLICENSETERMS="True"`若要接受授權合約的個別 Python


> [!NOTE]
> 您無法在 SQL Server 安裝程式中使用參數，針對 [啟動列] 變更服務帳戶。 我們建議您安裝使用預設的服務帳戶，並修改使用 SQL Server 組態管理員的服務帳戶。 之後，請務必重新啟動控制板服務。

## <a name="see-also"></a>另請參閱

[安裝 Microsoft R Server](https://docs.microsoft.com/r-server/install/r-server-install-windows)

R 服務支援小組的這篇文章會示範如何在 SQL Server 2016 執行自動的安裝或升級 R 服務：[沒有網際網路存取的電腦上部署 R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。
