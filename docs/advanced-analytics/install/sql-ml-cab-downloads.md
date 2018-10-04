---
title: CAB 下載 SQL Server 累計更新 |Microsoft Docs
description: SQL Server 2017 Machine Learning 服務和 SQL Server 2016 R Services 的 CAB 下載。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 25568dc5a76283b18affd10ef0419f83515f6403
ms.sourcegitcommit: 615f8b5063aed679495d92a04ffbe00451d34a11
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48232602"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>下載 SQL Server 資料庫內分析的累計更新的執行個體的封包

已針對資料庫內分析的 SQL Server 執行個體包含 R 和 Python 的功能。 這些功能提供在封包檔安裝，並透過 SQL Server 安裝程式提供服務。 在連線網際網路的裝置，通常會透過 Windows Update 套用封包更新。 在中斷連線的伺服器，必須下載並手動套用封包檔。 

本文提供每個累計更新的封包檔的下載連結。 SQL Server 2017 Machine Learning 服務 （R 和 Python），以及 SQL Server 2016 R Services 會提供連結。 如需離線安裝的詳細資訊，請參閱[安裝 SQL Server 機器學習服務沒有網際網路存取元件](sql-ml-component-install-without-internet-access.md#apply-cu)。

## <a name="prerequisites"></a>先決條件

基準安裝開始。

+ SQL Server 2017 Machine Learning 服務，在初始版本會為基準安裝。 
+ 在 SQL Server 2016 R Services，您可以開始初始版本、 SP1 或 SP2。 

您也可以將累計更新套用到在獨立伺服器。

## <a name="sql-server-2017-cabs"></a>SQL Server 2017 Cab

封包檔會依反向時間順序列出。 當您下載的封包檔，並將它們傳送到目標電腦上時，將它們放置在方便存取的資料夾中這類**下載**或安裝程式使用者的 %temp%資料夾。

版本  |下載連結  | 已解決的問題 | 
---------|---------------|-------|
**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)-[CU11](https://support.microsoft.com/help/4462262)** |  |  |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 從舊版本未變更。 |
R 伺服器      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| 微幅修正。|
Microsoft Python 開放     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版本未變更。 |
Python 伺服器    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| 移除重複項目時，Python rx_data_step 會遺失資料列順序。 <br/>SPEE 無法在叢集資料行存放區索引上的資料類型偵測。 <br/>資料行包含所有 null 值時，會傳回空白資料表。 |
**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 從舊版本未變更。 |
R 伺服器      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
Microsoft Python 開放     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版本未變更。 |
Python 伺服器    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 從舊版本未變更。 |
R 伺服器      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
Microsoft Python 開放     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版本未變更。 |
Python 伺服器    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| SPEES 查詢中的日期時間資料類型。<br/>預先定型的模型遺漏時，改善 microsoftml 中的錯誤訊息。<br/> 修正 revoscalepy 轉換函式和變數。|
**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 從舊版本未變更。 |
R 伺服器      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| RxInstallPackages 中的長時間的路徑相關錯誤。<br/>RxExec 中回送連接。
Microsoft Python 開放    | 從舊版本未變更。 |
Python 伺服器    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>在針對 rx_exec 回送連接。
**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |
Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 從舊版本未變更。 |
R 伺服器      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
Microsoft Python 開放     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版本未變更。 |
 Python 伺服器    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
**[SQL Server 2017 cu3 起](https://support.microsoft.com/help/4052987)** |  |  |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
R 伺服器      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
Microsoft Python 開放     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版本未變更。 |
Python 伺服器    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| Python 模型序列化 revoscalepy，使用[rx_serialize_model 函式](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)。<br/>[原生評分](../sql-native-scoring.md)支援，以及增強[即時評分](../real-time-scoring.md)。 
**SQL Server 2017 [CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |
Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| 從舊版本未變更。 |
R 伺服器      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Microsoft Python 開放     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版本未變更。 | 
Python 伺服器    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | 新增 rx_create_col_info 傳回結構描述資訊。 <br/>增強[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)以支援平行處理的案例使用`RxLocalParallel`計算內容。|
**初始版本** |  |  |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
R 伺服器      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python 開放     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Python 伺服器    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |


<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>SQL Server 2016 Cab

SQL Server 2016 R services，基準版本是 RTM 版本或 service pack 版本。

版本  |下載連結  |
---------|---------------|
**SQL Server 2016 SP2 CU1 CU2**     |
Microsoft R Open     |[SRO_3.2.2.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039)|
Microsoft R Server    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
**SQL Server 2016 SP1 CU4 CU10**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP1 CU1 CU3**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 CU4 CU9**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU2 CU3**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**SQL Server 2016 CU1**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)

> [!NOTE]
> 
> 當離線，請安裝 SQL Server 2016 SP1 CU4 或 SP1 CU5，下載 SRO_3.2.2.16000_1033.cab。 如果安裝程式 對話方塊中所示，您可以下載從 FWLINK 831785 的 SRO_3.2.2.13000_1033.cab，重新為 SRO_3.2.2.16000_1033.cab 命名檔案，然後再安裝累計更新。

如果您想要檢視適用於 Microsoft R 的原始程式碼，它是可供下載以格式為.tar 封存：[下載 R Server 安裝程式](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

## <a name="see-also"></a>另請參閱

[在沒有網際網路存取的電腦上套用累計更新](sql-ml-component-install-without-internet-access.md#apply-cu)

[在具有網際網路連線的電腦上套用累計更新](sql-ml-component-install-without-internet-access.md#apply-cu)

[累計更新套用到在獨立伺服器](sql-machine-learning-standalone-windows-install.md#apply-cu)
