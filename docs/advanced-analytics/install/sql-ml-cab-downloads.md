---
title: 下載離線安裝的更新
description: 下載適用於 SQL Server 機器學習服務的 Python 與 R CAB 檔案。 這些 CAB 檔案包含機器學習服務 (Python 與 R) 功能的更新，當您在無法存取網際網路的伺服器上安裝 SQL Server 時就會使用這些檔案。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/13/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7b50e11995cc1f07b848a460ecd096f97d7b7f9b
ms.sourcegitcommit: 49082f9b6b3bc8aaf9ea3f8557f40c9f1b6f3b0b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2020
ms.locfileid: "77256675"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-machine-learning-services"></a>適用於 SQL Server 機器學習服務之累積更新的 CAB 下載

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
下載適用於 SQL Server 機器學習服務的 Python 與 R CAB 檔案。 這些 CAB 檔案包含機器學習服務 (Python 與 R) 功能的更新，當您在無法存取網際網路的伺服器上安裝 SQL Server 時就會使用這些檔案。
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
下載適用於 SQL Server 2016 R Services 的 Python 與 R CAB 檔案。 這些 CAB 檔案包含 R Services 功能的更新，當您在無法存取網際網路的伺服器上安裝 SQL Server 時就會使用這些檔案。
::: moniker-end

您將可在下方找到適用於每個累積更新之 CAB 檔案的下載連結。 如需有關離線安裝的詳細資訊，請參閱[在無法存取網際網路的情況下安裝 SQL server 機器學習元件](sql-ml-component-install-without-internet-access.md#apply-cu)。

## <a name="prerequisites"></a>Prerequisites

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
從基準安裝開始。 在 SQL Server 機器學習服務上，初始版本是基準安裝。 
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
從基準安裝開始。  在 SQL Server 2016 R Services 上，您可以從初始版本、SP1 或 SP2 開始。 
::: moniker-end

您也可以套用累積更新。

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

## <a name="sql-server-2017-cabs"></a>SQL Server 2017 CAB

CAB 檔案會以反向時間順序列出。 當您下載 CAB 檔並將它們傳輸到目標電腦時，請將它們放在方便的資料夾中，例如 [下載]  或安裝使用者的 %temp% 資料夾。

|版本  |元件 | 下載連結  | 解決的問題 | 
|---------|----------|----------------|------------------|
|**[SQL Server 2017 CU19](https://support.microsoft.com/en-us/help/4535007/)** |  |  |  |
| | Microsoft R Open | [SRO_3.3.3.1900_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2106367&clcid=1033) | 修正 Bug：`sp_execute_external_script` 執行 R 指令碼會顯示警告訊息 |
| | R 伺服器| [SRS_9.2.0.1900_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2106460&clcid=1033) | 從舊版到現在都沒有變更。 |
| | Microsoft Python Open | [SPO_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073897&clcid=1033) | 從舊版到現在都沒有變更。 |
| | Python Server | [SPS_9.2.0.1900_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2106459&clcid=1033) | 修正 Bug：以 OutputDataSet 格式將 Varbinary 或 binary 資料類型傳回 SQL Server 時，`sp_execute_external_script` 執行 python 指令碼有時會遺失資料。 |
|**[SQL Server 2017 CU14](https://support.microsoft.com/help/4484710/)-[CU15](https://support.microsoft.com/help/4498951/)-[CU16](https://support.microsoft.com/help/4508218/)-[CU17](https://support.microsoft.com/en-us/help/4515579/)-[CU18](https://support.microsoft.com/en-us/help/4527377/)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073898&clcid=1033)| 套件內的二進位檔案現在已簽署。 |
| | R 伺服器      |[SRS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2069739&clcid=1033)| 套件內的二進位檔案現在已簽署。 |
| | Microsoft Python Open     | [SPO_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073897&clcid=1033)| 套件內的二進位檔案現在已簽署。 |
| | Python Server    |[SPS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2071421&clcid=1033)| 套件內的二進位檔案現在已簽署。  |
|**[SQL Server 2017 CU13](https://support.microsoft.com/help/4466404)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 從舊版到現在都沒有變更。 |
| | R 伺服器      |[SRS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038263&clcid=1033)| 包含用於升級[運作獨立 R Server](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)的修正程式，就像透過 SQL Server 安裝程式安裝一樣。 使用 CU13 CAB，並遵循[這些指示](sql-machine-learning-standalone-windows-install.md#apply-cu)以套用更新。 |
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版到現在都沒有變更。 |
| | Python Server    |[SPS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038197&clcid=1033)| 包含用於升級[運作獨立 Python Server](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)的修正程式，就像透過 SQL Server 安裝程式安裝一樣。 使用 CU13 CAB，並遵循[這些指示](sql-machine-learning-standalone-windows-install.md#apply-cu)以套用更新。 |
|**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)-[CU11](https://support.microsoft.com/help/4462262)-[CU12](https://support.microsoft.com/help/4464082)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 從舊版到現在都沒有變更。 |
| | R 伺服器      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| 微幅修正。|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版到現在都沒有變更。 |
| | Python Server    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| 移除重複項時，Python rx_data_step 會失去資料列順序。 <br/>SPEE 在叢集資料行存放區索引上的資料類型偵測失敗。 <br/>當資料行包含所有 Null 值時，會傳回空資料表。 |
|**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 從舊版到現在都沒有變更。 |
| | R 伺服器      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版到現在都沒有變更。 |
| | Python Server    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
|**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 從舊版到現在都沒有變更。 |
| | R 伺服器      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版到現在都沒有變更。 |
| | Python Server    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| SPEES 查詢中的日期時間資料類型。<br/>已改善預先定型模型遺失時，microsoftml 中的錯誤訊息。<br/> 已修正 revoscalepy 轉換函式與變數。|
|**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 從舊版到現在都沒有變更。 |
| | R 伺服器      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| RxInstallPackages 中的長路徑相關錯誤。<br/>RxExec 的回送中的連線。
| | Microsoft Python Open    | 從舊版到現在都沒有變更。 |
| | Python Server    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>rx_exec 的回送中的連線。
|**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 從舊版到現在都沒有變更。 |
| | R 伺服器      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版到現在都沒有變更。 |
| |  Python Server    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
|**[SQL Server 2017 CU3](https://support.microsoft.com/help/4052987)** |  |  |  |
| | Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
| | R 伺服器      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版到現在都沒有變更。 |
| | Python Server    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| revoscalepy 中的 Python 模型序列化 (使用 [rx_serialize_model 函式](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model))。<br/>[原生評分](../sql-native-scoring.md)支援，加上[即時評分](../real-time-scoring.md)加強功能。 
|**[SQL Server 2017 CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| 從舊版到現在都沒有變更。 |
| | R 伺服器      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
| | Microsoft Python Open     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 從舊版到現在都沒有變更。 | 
| | Python Server    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | 針對傳回結構描述資訊新增 rx_create_col_info。 <br/>[rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) 的增強功能，以支援使用 `RxLocalParallel` 計算內容的平行案例。|
|**初始版本** |  |  |
| | Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
| | R 伺服器      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
| | Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
| | Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>SQL Server 2016 CABs

針對 SQL Server 2016 R Services，基準版本為 RTM 版本或 Service Pack 版本。

|版本  |下載連結  |
|---------|---------------|
|**SQL Server 2016 SP2 CU6**     |
|Microsoft R Open     |[SRO_3.2.2.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079936&clcid=1033)|
|Microsoft R 伺服器    |[SRS_8.0.3.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079933&clcid=1033)|
|**SQL Server 2016 SP2 CU1-CU5**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R 伺服器    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
|**SQL Server 2016 SP2**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R 伺服器    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)|
|**SQL Server 2016 SP1 CU14**     |
|Microsoft R Open     |[SRO_3.2.2.16100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2080130&clcid=1033)|
|Microsoft R 伺服器    |[SRS_8.0.3.17200_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079935&clcid=1033)|
|**SQL Server 2016 SP1 CU1-CU13**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R 伺服器    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
|**SQL Server 2016 SP1**     |
|Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)|
|Microsoft R 伺服器     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)|
|**SQL Server 2016 CU4-CU9**     |
|Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
|Microsoft R 伺服器     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
|**SQL Server 2016 CU2-CU3**     |
|Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)|
|Microsoft R 伺服器     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)|
|**SQL Server 2016 CU1**     |
|Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)|
|Microsoft R 伺服器     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)|
|**SQL Server 2016 RTM**     |
|Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)|
|Microsoft R 伺服器     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)|

> [!NOTE]
> 
> 當您離線安裝 SQL Server 2016 SP1 CU4 或 SP1 CU5 時，請下載 SRO_3.2.2.16000_1033.cab。 如果您已如安裝程式對話方塊所示，從 FWLINK 831785 下載 SRO_3.2.2.13000_1033.cab，請在安裝累積更新之前，先將檔案重新命名為 SRO_3.2.2.16000_1033.cab。

若要檢視 Microsoft R 的原始程式碼，可以將其下載為. tar 格式的封存：[下載 R Server 2安裝程式](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

::: moniker-end

## <a name="next-steps"></a>後續步驟

[在無法存取網際網路的電腦上套用累積更新](sql-ml-component-install-without-internet-access.md#apply-cu)

[在可以存取網際網路的電腦上套用累積更新](sql-ml-component-install-without-internet-access.md#apply-cu)

[將累積更新套用到獨立伺服器](sql-machine-learning-standalone-windows-install.md#apply-cu)
