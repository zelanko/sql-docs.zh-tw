---
title: CAB 下載 SQL Server 累計更新 |Microsoft Docs
description: SQL Server 2017 Machine Learning 服務和 SQL Server 2016 R Services 的 CAB 下載。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/28/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 57481eaee3ee6de5816e69edda2936d4ee30fc49
ms.sourcegitcommit: e4e9f02b5c14f3bb66e19dec98f38c012275b92c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2018
ms.locfileid: "43118281"
---
# <a name="cab-downloads-for-cumulative-updates-of-sql-server-in-database-analytics-instances"></a>下載 SQL Server 資料庫內分析的累計更新的執行個體的封包

SQL Server 執行個體設定為在資料庫內分析包括 R 和 Python 的功能隨附於封包檔，安裝並透過服務的 SQL Server 安裝程式。 

在伺服器上連線到網際網路，通常會透過 Windows Update 套用 CAB 更新。 已中斷連線的伺服器必須手動更新。 如需離線安裝指示，請參閱[安裝 SQL Server 機器學習服務沒有網際網路存取元件](sql-ml-component-install-without-internet-access.md)。

本文章會提供每個 SQL Server 2017 Machine Learning 服務 （R 和 Python）-或 SQL Server 2016 R Services-的累計更新的封包檔的下載連結，以便您可以手動更新與網際網路中斷連線的伺服器。 

## <a name="prerequisites"></a>先決條件

基準安裝開始。

+ SQL Server 2017 Machine Learning 服務，在初始版本會為基準安裝。 
+ 在 SQL Server 2016 R Services，您可以開始初始版本、 SP1 或 SP2。 

接下來，套用[累計更新](https://support.microsoft.com/help/4047329)SQL Server 資料庫引擎執行個體。

您有基準安裝，並已套用累計更新至 SQL Server 之後，您可以執行[匯集升級](sql-ml-component-install-without-internet-access.md#slipstream-upgrades)安裝封包檔，以更新機器學習服務功能。

封包檔會依反向時間順序列出。 當您下載的封包檔，並將它們傳送到目標電腦上時，將它們放置在方便存取的資料夾中這類**下載**或安裝程式使用者的 %temp%資料夾。

## <a name="sql-server-2017-cabs"></a>SQL Server 2017 Cab

版本  |下載連結  | 修正 | 
---------|---------------|-------|
**[CU10](https://support.microsoft.com/help/4342123)** |  |  |
Microsoft R Open     |沒有變更;使用先前[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)| |
R 伺服器      |[SRS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006287&clcid=1033)| 微幅修正。|
Microsoft Python 開放     |沒有變更;使用先前[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)| |
Python 伺服器    |[SPS_9.2.0.1000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=2006805&clcid=1033)| 移除重複項目時，Python rx_data_step 會遺失資料列順序。 <br/>Python SPEE 會在取得資料類型從叢集資料行存放區索引，在某些情況下失敗。 <br/>資料行包含所有 null 值時，Python 會傳回空白資料表。 |
**[CU8](https://support.microsoft.com/help/4338363)-[CU9](https://support.microsoft.com/help/4341265)** |
Microsoft R Open     |沒有變更;使用先前[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
R 伺服器      |[SRS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874708&clcid=1033)|
Microsoft Python 開放     |沒有變更;使用先前[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)|
Python 伺服器    |[SPS_9.2.0.800_1033.cab](https://go.microsoft.com/fwlink/?LinkId=874707&clcid=1033)]|
**[CU6](https://support.microsoft.com/help/4101464)-[CU7](https://support.microsoft.com/help/4229789)** |
Microsoft R Open     |沒有變更;使用先前[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
R 伺服器      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
Microsoft Python 開放     |沒有變更;使用先前[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)|
Python 伺服器    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)|
**[CU5](https://support.microsoft.com/help/4092643)** |
Microsoft R Open     |沒有變更;使用先前[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
R 伺服器      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)|
Microsoft Python 開放     |沒有變更;使用先前[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)|
Python 伺服器    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)|
**[CU4](https://support.microsoft.com/help/4056498)** |
Microsoft R Open     |沒有變更;使用先前[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
R 伺服器      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
Microsoft Python 開放     |沒有變更;使用先前[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)|
 Python 伺服器    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
**[CU3](https://support.microsoft.com/help/4052987)** |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
R 伺服器      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
Microsoft Python 開放     |沒有變更;使用先前[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)|
Python 伺服器    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)|
**[CU1](https://support.microsoft.com/help/4038634)-[CU2](https://support.microsoft.com/help/4052574)** |
Microsoft R Open     |沒有變更;使用先前[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
R 伺服器      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Microsoft Python 開放     |沒有變更;使用先前[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502)|
Python 伺服器    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) |
**初始版本** |
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
Microsoft R Open     |沒有變更;使用先前[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP1 CU1 CU3**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)=
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

# <a name="see-also"></a>另請參閱

[安裝 SQL Server machine learning 沒有網際網路存取的元件](sql-ml-component-install-without-internet-access.md)
