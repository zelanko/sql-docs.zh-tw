---
title: 安裝 SQL Server 機器學習元件沒有網際網路存取 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/02/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a0ec6834bf3aee8a7f8176bc5fd6d6d66d367b62
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="install-sql-server-machine-learning-components-without-internet-access"></a>安裝 SQL Server 機器學習服務沒有網際網路存取的元件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

根據預設，連接到 Microsoft 下載網站，取得必要的安裝程式和更新的元件的機器學習 SQL Server 上。 如果防火牆限制防止安裝程式，使其無法到達這些站台，您可以使用網際網路連線的裝置下載檔案，檔案傳送給離線的伺服器，然後執行安裝程式。

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

> [!NOTE]  
> 如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。  
 
 ###  <a name="bkmk_ga_instalpatch"></a> 安裝修補程式需求 

Microsoft 發現特定版本的 Microsoft VC++ 2013 Runtime 二進位檔問題，SQL Server 必須安裝這些二進位檔。 如果未安裝 VC Runtime 二進位檔的這項更新，SQL Server 就可能在特定情況下遇到穩定性問題。 安裝 SQL Server 之前，請先遵循 [SQL Server 版本資訊](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)的指示，查看您的電腦是否需要 VC Runtime 二進位檔的修補程式。  


## <a name="download-cab-files"></a>下載的.cab 檔

在連線網際網路的伺服器上，下載進行離線安裝所需的.cab 檔案。 安裝程式會使用.cab 檔案來安裝附加的功能。

版本  |下載連結  |
---------|---------|
**SQL Server 2017 初始版本** |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
開啟 Microsoft Python     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python 伺服器    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |
**SQL Server 2017 CU1** |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
開啟 Microsoft Python     |不是變更，使用上一個 |
Microsoft Python 伺服器    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) |
**SQL Server 2017 CU2** |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server      |不是變更，使用上一個|
開啟 Microsoft Python     |不是變更，使用上一個|
Microsoft Python 伺服器    |不是變更，使用上一個|
**SQL Server 2017 CU3** |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
開啟 Microsoft Python     |不是變更，使用上一個|
Microsoft Python 伺服器    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)|
**SQL Server 2017 CU4** |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
開啟 Microsoft Python     |不是變更，使用上一個|
Microsoft Python 伺服器    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
**SQL Server 2017 CU5** |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)|
開啟 Microsoft Python     |不是變更，使用上一個|
Microsoft Python 伺服器    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)|
**SQL Server 2017 cu6 來** |
Microsoft R Open     |不是變更，使用上一個|
Microsoft R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
開啟 Microsoft Python     |不是變更，使用上一個|
Microsoft Python 伺服器    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)|

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

## <a name="transfer-files"></a>非同步傳送檔案

壓縮的 SQL Server 安裝媒體，您已下載至安裝安裝程式的電腦的檔案傳輸。

例如放在方便存取的資料夾中的封包檔**下載**或安裝程式使用者的 temp 資料夾： < 使用者名稱 > C:\Users \AppData\Local\Temp。

En_sql_server_2017.iso 檔案放入方便存取的資料夾。 按兩下**setup.exe**以開始安裝。

### <a name="run-setup"></a>執行安裝程式

當您與網際網路中斷連線的電腦上執行 SQL Server 安裝程式時，安裝程式會加入**離線安裝**精靈頁面上，好讓您可以指定您在上一個步驟中複製.cab 檔案的位置。

1. 啟動 SQL Server 安裝精靈。

2. 當安裝精靈顯示開放原始碼 R 或 Python 元件的授權頁面時，按一下 **接受**。 接受授權條款，可讓您繼續進行下一個步驟。

3. 在**離線安裝**頁面上，於**安裝路徑**，指定包含您之前複製的.cab 檔案的資料夾。

4. 繼續下列螢幕上的提示完成安裝。

安裝完成之後，重新啟動服務，然後設定伺服器，以啟用執行指令碼中所述[安裝 SQL Server 2017 機器學習服務 （資料庫）](sql-machine-learning-services-windows-install.md)或[安裝 SQL Server2016 R 服務 （資料庫）](sql-r-services-windows-install.md)。

## <a name="slipstream-upgrades-for-offline-servers"></a>匯集升級為離線的伺服器的

匯集安裝程式是指將補充程式或更新套用至失敗的執行個體安裝，以修正現有問題的功能。 這個方法的優點是在您執行安裝程式的同時更新 SQL Server，以避免稍後分別重新啟動。

+ 如果伺服器無法存取網際網路，您必須在更新程序開始「之前」下載 SQL Server 安裝程式，然後下載對應的 R 元件安裝程式版本。  根據預設，使用 SQL Server 不包含的 R 元件。

+ 如果您要將這些元件加入現有安裝，請使用更新的版本的 SQL Server 安裝程式，以及對應的其他元件的更新的版本。 當您指定 R 功能是要安裝時，安裝程式會尋找符合的機器學習服務元件的安裝程式的版本。

## <a name="get-help"></a>取得說明

需要協助以安裝或升級嗎？ 常見的問題和已知的問題的解答，請參閱下列文章：

* [升級及安裝常見問題集-機器學習服務](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要檢查執行個體的安裝狀態，並修正常見的問題，請嘗試這些自訂報表。

* [SQL Server R services 的自訂報表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

R 服務支援小組的這篇文章會示範如何在 SQL Server 2016 執行自動的安裝或升級 R 服務：[沒有網際網路存取的電腦上部署 R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。


## <a name="next-steps"></a>後續的步驟

R 開發人員可以開始使用一些簡單的案例，並了解 R 與 SQL Server 的運作方式的基本概念。 下一個步驟中，請參閱下列連結：

+ [教學課程： 在 T-SQL 中執行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R 開發人員的教學課程： 在資料庫分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開發人員可以瞭解如何使用 SQL Server 中的 Python，依照這些教學課程：

+ [教學課程： 在 T-SQL 中執行 Python](../tutorials/run-python-using-t-sql.md)
+ [Python 開發人員的教學課程： 在資料庫分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要檢視的機器學習，根據真實世界案例的範例，請參閱[機器學習教學課程](../tutorials/machine-learning-services-tutorials.md)。

