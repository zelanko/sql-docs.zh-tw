---
title: 組態設定 （SQL Server 資料移轉小幫手） |Microsoft 文件
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 4b42f816755b312f95609bd25ac6122b8fbf321c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32867203"
---
# <a name="configuration-settings-for-data-migration-assistant"></a>資料移轉小幫手的組態設定

您可以微調特定行為的資料移轉小幫手 dma.exe.config 檔案中使用組態值。 本文中的索引鍵的組態值。

在您的電腦上的下列資料夾中，您可以在資料移轉小幫手的桌面應用程式和命令列公用程式找到 dma.exe.config 檔案。

- 桌面應用程式

  %Programfiles%\\Microsoft 資料移轉小幫手\\dma.exe.config

- 命令列公用程式

  %Programfiles%\\Microsoft 資料移轉小幫手\\dmacmd.exe.config 

請務必儲存原始的組態檔的複本，然後再進行任何修改。 完成變更之後，重新啟動資料移轉小幫手，新的組態值才會生效。

## <a name="number-of-databases-to-assess-in-parallel"></a>若要評估以平行方式的資料庫數目

資料移轉小幫手，評估多個資料庫，以平行方式。 在評估期間的資料移轉小幫手會擷取資料層應用程式 (dacpac) 若要了解資料庫結構描述。 如果同一部伺服器上的多個資料庫都會以平行方式進行評估，這項作業可以逾時。 

資料移轉小幫手 2.0 版開始，您可以控制這藉由設定 parallelDatabases 組態值。 預設值為 8。

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>若要以平行方式移轉的資料庫數目

資料移轉小幫手移轉多個資料庫，以平行方式，之前移轉的登入。 在移轉期間，資料移轉小幫手會進行來源資料庫的備份、 選擇性地複製備份，然後還原它在目標伺服器上。 多個資料庫選取進行移轉時，您可能會發生逾時失敗。 

資料移轉小幫手的 2.0 版開始，如果您遇到這個問題可以減少 parallelDatabases 組態值。 您可以增加要縮短整體移轉時間的值。

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases=”8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>DacFX 設定

在評估期間資料移轉小幫手會擷取資料層應用程式 (dacpac) 若要了解資料庫結構描述。 這項作業可能會因逾時為極大型資料庫，或如果伺服器是在負載之下。 從資料移轉 v1.0 開始，您可以修改下列設定值，以避免錯誤。 

> [!NOTE]
> 整個&lt;dacfx&gt;標記為預設註解項目。 移除註解，然後視需要修改值。

- CommandTimeout

   這會設定 IDbCommand.CommandTimeout 屬性*秒*。 (預設值 = 60)

- databaseLockTimeout

   這相當於[設定鎖定\_逾時等候逾時\_期間](../t-sql/statements/set-lock-timeout-transact-sql.md)中*毫秒*。 (預設 = 5000)

- maxDataReaderDegreeOfParallelism

   若要使用的 SQL 連接集區連線的數目。 (預設值 = 8)

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```


## <a name="stretch-database-recommendation-threshold"></a>Stretch Database： 建議的臨界值

與[SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database)，您可以動態地延伸暖資料和冷交易資料從 Microsoft SQL Server 2016 到 Azure。 Stretch Database 目標交易資料庫包含大量原始資料。 Stretch Database 的建議事項，在儲存體功能的建議事項，先識別資料表其認定將受益於這項功能，然後用來識別需要以啟用這項功能的資料表進行的變更。

資料移轉小幫手 2.0 版開始，您可以控制此臨界值資料表的 Stretch Database 功能使用 recommendedNumberOfRows 組態值。 預設值為 100,000 個資料列。 如果您想要分析的延展功能，即使較小的資料表，然後據以降低值。

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>SQL 連接逾時

您可以控制[SQL 連接逾時](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx)時執行的連接逾時值設為指定的秒數的評估或移轉，來源和目標執行個體。 預設值為 15 秒。

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```


## <a name="see-also"></a>另請參閱

[資料移轉小幫手下載](https://www.microsoft.com/download/details.aspx?id=53595)
