---
title: 設定 Data Migration assistant (SQL Server) |Microsoft Docs
description: 了解如何設定的更新組態檔中的值設定 Data Migration Assistant
ms.custom: ''
ms.date: 08/29/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 87e81a1b73ac8b3af9b9c35449dc4966fc4cf285
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755576"
---
# <a name="configure-settings-for-data-migration-assistant"></a>設定 Data Migration assistant

您可以微調特定行為的資料移轉小幫手 dma.exe.config 檔案中設定組態值。 這篇文章描述的索引鍵的組態值。

您可以找到 dma.exe.config 檔案 Data Migration Assistant 的桌面應用程式和命令列公用程式，您的電腦上的下列資料夾中。

- 桌面應用程式

  %Programfiles%\\Microsoft Data Migration Assistant\\dma.exe.config

- 命令列公用程式

  %Programfiles%\\Microsoft Data Migration Assistant\\dmacmd.exe.config 

請務必儲存一份原始的組態檔進行任何修改之前的時間。 完成變更之後，重新啟動資料移轉小幫手做為新的組態值才會生效。

## <a name="number-of-databases-to-assess-in-parallel"></a>要評估以平行方式的資料庫數目

Data Migration Assistant 評估多個資料庫，以平行方式。 在評估期間 Data Migration Assistant 中擷取資料層應用程式 (dacpac) 以了解資料庫結構描述。 這項作業可以逾時，如果相同的伺服器上的多個資料庫以平行方式來評估。 

開始使用 Data Migration Assistant v2.0，您可以控制此設定 parallelDatabases 組態值。 預設值為 8。

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>若要以平行方式移轉的資料庫數目

Data Migration Assistant 移轉多個資料庫，以平行方式，之前移轉的登入。 在移轉期間，Data Migration Assistant 將進行來源資料庫的備份，選擇性地複製備份，並再將其還原目標伺服器上。 多個資料庫選取進行移轉時，您可能會發生逾時失敗。 

您可以使用 Data Migration Assistant v2.0，從開始，如果您遇到這個問題減少 parallelDatabases 組態值。 您可以增加要縮短整體的移轉時間的值。

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases=”8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>DacFX 設定

在評估期間 Data Migration Assistant 中擷取資料層應用程式 (dacpac) 以了解資料庫結構描述。 這項作業可能會因逾時的極大型資料庫，或如果伺服器是在負載之下。 從開始資料移轉 v1.0，您可以修改下列設定值，以避免發生錯誤。 

> [!NOTE]
> 將整個&lt;dacfx&gt;加上預設註解項目。 移除註解，然後再視需要修改值。

- commandTimeout

   這會設定 IDbCommand.CommandTimeout 屬性*秒*。 (預設值 = 60)

- databaseLockTimeout

   這相當於[設定的鎖定\_逾時等候逾時\_期間](../t-sql/statements/set-lock-timeout-transact-sql.md)中*毫秒*。 (預設 = 5000)

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

具有[SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database)，您可以動態延展暖資料與冷交易資料從 Microsoft SQL Server 2016 至 Azure。 Stretch Database 交易資料庫為目標與大量的冷資料。 Stretch Database 的建議事項，在儲存體功能建議，首先會找出資料表，它會認為將受益於這項功能，然後它會識別要啟用這項功能的資料表所需的變更。

您可以從開始使用 Data Migration Assistant v2.0，來控制此臨界值的資料表，以符合使用 recommendedNumberOfRows 組態值的 Stretch Database 功能。 預設值為 100,000 個資料列。 如果您想要分析變得更小的資料表的延展功能，然後據以降低的值。

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>SQL 連接逾時

您可以控制[SQL 連線逾時](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx)來源和目標執行個體同時執行評定或移轉，將連接逾時值設定為指定的秒數。 預設值為 15 秒。

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```


## <a name="see-also"></a>另請參閱

[資料移轉小幫手下載](https://www.microsoft.com/download/details.aspx?id=53595)
