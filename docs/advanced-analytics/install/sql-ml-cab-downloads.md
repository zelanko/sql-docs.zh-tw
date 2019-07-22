---
title: SQL Server 累積更新的 CAB 下載
description: 適用于 SQL Server 2017 Machine Learning 服務和 SQL Server 2016 R Services 的 R 和 Python CAB 和套件下載。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0fd6b624b024c51965420dd438b8eb9ec04fbafc
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344945"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>SQL Server 資料庫內分析實例之累計更新的 CAB 下載

針對資料庫內分析所設定的 SQL Server 實例包括 R 和 Python 功能。 這些功能會隨附于封包檔中, 並透過 SQL Server 安裝程式進行安裝和服務。 在連線到網際網路的裝置上, CAB 更新通常會透過 Windows Update 套用。 在中斷連線的伺服器上, 必須手動下載並套用 CAB 檔案。 

本文提供每個累計更新之 CAB 檔案的下載連結。 SQL Server 2017 Machine Learning 服務 (R 和 Python) 以及 SQL Server 2016 R Services 皆提供連結。 如需離線安裝的詳細資訊, 請參閱在[沒有網際網路存取的情況下安裝 SQL Server 機器學習元件](sql-ml-component-install-without-internet-access.md#apply-cu)。

## <a name="prerequisites"></a>先決條件

開始進行基準安裝。

+ 在 SQL Server 2017 Machine Learning 服務上, 初始版本是基準安裝。 
+ 在 SQL Server 2016 R Services 上, 您可以從初始版本、SP1 或 SP2 開始。 

您也可以將累計更新套用到獨立伺服器。

## <a name="sql-server-2017-cabs"></a>SQL Server 2017 Cab

CAB 檔案會以反向時間順序列出。 當您下載封包檔並將它們傳送到目的電腦時, 請將它們放在方便的資料夾中, 例如**下載**或安裝使用者的% temp% 資料夾。

|版本  |元件 | 下載連結  | 解決的問題 | 
|---------|----------|----------------|------------------|
|**[SQL Server 2017 CU14](https://support.microsoft.com/help/4484710/)-[CU15](https://support.microsoft.com/help/4498951/)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073898&clcid=1033)| 封裝內的二進位檔現在已經過簽署。 |
| | R 伺服器      |[SRS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2069739&clcid=1033)| 封裝內的二進位檔現在已經過簽署。 |
| | Microsoft Python 開啟     | [SPO_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2073897&clcid=1033)| 封裝內的二進位檔現在已經過簽署。 |
| | Python 伺服器    |[SPS_9.2.0.1400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2071421&clcid=1033)| 封裝內的二進位檔現在已經過簽署。  |
|**[SQL Server 2017 CU13](https://support.microsoft.com/help/4466404)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 先前版本沒有任何變更。 |
| | R 伺服器      |[SRS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038263&clcid=1033)| 包含升級[運作獨立 R 伺服器](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)的修正程式, 透過 SQL Server 安裝程式安裝。 使用 CU13 Cab, 並遵循[這些指示](sql-machine-learning-standalone-windows-install.md#apply-cu)來套用更新。 |
| | Microsoft Python 開啟     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 先前版本沒有任何變更。 |
| | Python 伺服器    |[SPS_9.2.0.1300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2038197&clcid=1033)| 包含升級[運作獨立 Python 伺服器](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)的修正程式, 如透過 SQL Server 安裝程式安裝。 使用 CU13 Cab, 並遵循[這些指示](sql-machine-learning-standalone-windows-install.md#apply-cu)來套用更新。 |
|**[SQL Server 2017 CU10](https://support.microsoft.com/help/4342123)-[CU11](https://support.microsoft.com/help/4462262)-[CU12](https://support.microsoft.com/help/4464082)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 先前版本沒有任何變更。 |
| | R 伺服器      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| 微幅修正。|
| | Microsoft Python 開啟     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 先前版本沒有任何變更。 |
| | Python 伺服器    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| 移除重複專案時, Python rx_data_step 會失去資料列順序。 <br/>SPEE 在叢集資料行存放區索引上的 datatype 偵測失敗。 <br/>當資料行包含所有 null 值時, 會傳回空的資料表。 |
|**[SQL Server 2017 CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 先前版本沒有任何變更。 |
| | R 伺服器      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
| | Microsoft Python 開啟     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 先前版本沒有任何變更。 |
| | Python 伺服器    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)|
|**[SQL Server 2017 CU6](https://support.microsoft.com/help/4101464) - [CU7](https://support.microsoft.com/help/4229789)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 先前版本沒有任何變更。 |
| | R 伺服器      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
| | Microsoft Python 開啟     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 先前版本沒有任何變更。 |
| | Python 伺服器    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)| SPEES 查詢中的日期時間資料類型。<br/>已改善預先定型模型遺失時 microsoftml 中的錯誤訊息。<br/> 修正 revoscalepy 轉換函式和變數的問題。|
|**[SQL Server 2017 CU5](https://support.microsoft.com/help/4092643)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 先前版本沒有任何變更。 |
| | R 伺服器      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)| RxInstallPackages 中的長路徑相關錯誤。<br/>RxExec 的回送中的連接。
| | Microsoft Python 開啟    | 先前版本沒有任何變更。 |
| | Python 伺服器    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)| <br/>Rx_exec 的回送中的連接。
|**[SQL Server 2017 CU4](https://support.microsoft.com/help/4056498)** |  |   |  |
| | Microsoft R Open     | [SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| 先前版本沒有任何變更。 |
| | R 伺服器      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
| | Microsoft Python 開啟     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 先前版本沒有任何變更。 |
| |  Python 伺服器    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
|**[SQL Server 2017 CU3](https://support.microsoft.com/help/4052987)** |  |  |  |
| | Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
| | R 伺服器      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
| | Microsoft Python 開啟     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 先前版本沒有任何變更。 |
| | Python 伺服器    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)| 使用[rx_serialize_model 函數](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model), 在 revoscalepy 中進行 Python 模型序列化。<br/>[原生評分](../sql-native-scoring.md)支援, 加上[即時評分](../real-time-scoring.md)的增強功能。 
|**[SQL Server 2017 CU1](https://support.microsoft.com/help/4038634) - [CU2](https://support.microsoft.com/help/4052574)** |  |  |  |
| | Microsoft R Open     | [SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)| 先前版本沒有任何變更。 |
| | R 伺服器      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
| | Microsoft Python 開啟     | [SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| 先前版本沒有任何變更。 | 
| | Python 伺服器    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) | 加入 rx_create_col_info 以傳回架構資訊。 <br/>[Rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)的增強功能, 可支援使用計算`RxLocalParallel`內容的平行案例。|
|**初始版本** |  |  |
| | Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
| | R 伺服器      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
| | Microsoft Python 開啟     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
| | Python 伺服器    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |


<a name="bkmk_2016Installers"></a>

## <a name="sql-server-2016-cabs"></a>SQL Server 2016 Cab

針對 SQL Server 2016 R 服務, 基準版本為 RTM 版本或 Service Pack 版本。

|版本  |下載連結  |
|---------|---------------|
|**SQL Server 2016 SP2 CU6**     |
|Microsoft R Open     |[SRO_3.2.2.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079936&clcid=1033)|
|Microsoft R Server    |[SRS_8.0.3.20100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079933&clcid=1033)|
|**SQL Server 2016 SP2 CU1-CU5**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038)|
|**SQL Server 2016 SP2**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)|
|**SQL Server 2016 SP1 CU14**     |
|Microsoft R Open     |[SRO_3.2.2.16100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2080130&clcid=1033)|
|Microsoft R Server    |[SRS_8.0.3.17200_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2079935&clcid=1033)|
|**SQL Server 2016 SP1 CU1-CU13**     |
|Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
|Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
|**SQL Server 2016 SP1**     |
|Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)|
|Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)|
|**SQL Server 2016 CU4-CU9**     |
|Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
|Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
|**SQL Server 2016 CU2-CU3**     |
|Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)|
|Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)|
|**SQL Server 2016 CU1**     |
|Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)|
|Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)|
|**SQL Server 2016 RTM**     |
|Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)|
|Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)|

> [!NOTE]
> 
> 當您離線安裝 SQL Server 2016 SP1 CU4 或 SP1 CU5 時, 請下載 SRO_ 3.2.2.16000 _1033 .cab。 如果您已依照 [安裝程式] 對話方塊中的指示, 從 FWLINK 831785 下載 SRO_ 3.2.2.13000 _1033, 請在安裝累積更新之前, 將檔案重新命名為 SRO_ 3.2.2.16000 _1033 .cab。

如果您想要查看 Microsoft R 的原始程式碼, 可以將其下載為. tar 格式的封存:[下載 R Server 安裝程式](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

## <a name="see-also"></a>另請參閱

[在沒有網際網路存取的電腦上套用累計更新](sql-ml-component-install-without-internet-access.md#apply-cu)

[在具有網際網路連線能力的電腦上套用累計更新](sql-ml-component-install-without-internet-access.md#apply-cu)

[將累計更新套用到獨立伺服器](sql-machine-learning-standalone-windows-install.md#apply-cu)
