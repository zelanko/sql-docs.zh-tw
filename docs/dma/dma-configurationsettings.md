---
title: 設定 Data Migration Assistant 的設定
description: 瞭解如何藉由更新設定檔中的值，來設定 Data Migration Assistant 的設定
ms.custom: seo-lt-2019
ms.date: 03/12/2019
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
ms.openlocfilehash: fc280fa541e2a6b5ea984086d694ffdd3f7c39a8
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056545"
---
# <a name="configure-settings-for-data-migration-assistant"></a>設定 Data Migration Assistant 的設定

您可以藉由在 cmd.exe .config 檔案中設定設定值，微調 Data Migration Assistant 的特定行為。 本文說明主要設定值。

您可以在電腦上的下列資料夾中，找到 Data Migration Assistant 桌面應用程式和命令列公用程式的 cmd.exe .config 檔案。

- 桌面應用程式

  % ProgramFiles%\\Microsoft Data Migration Assistant\\的 dism.exe .config

- 命令列公用程式

  % ProgramFiles%\\Microsoft Data Migration Assistant\\dmacmd .exe .config 

請務必先儲存原始設定檔案的複本，再進行任何修改。 進行變更之後，請重新開機 Data Migration Assistant，新的設定值才會生效。

## <a name="number-of-databases-to-assess-in-parallel"></a>要平行評估的資料庫數目

Data Migration Assistant 會以平行方式評估多個資料庫。 在評估期間 Data Migration Assistant 會將資料層應用程式（dacpac）解壓縮，以瞭解資料庫架構。 如果同一部伺服器上的多個資料庫以平行方式進行評估，此作業可能會超時。 

從 Data Migration Assistant v2.0 開始，您可以藉由設定 parallelDatabases 設定值來控制此項。 預設值為8。

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>要平行遷移的資料庫數目

Data Migration Assistant 在遷移登入之前，平行遷移多個資料庫。 在遷移期間，Data Migration Assistant 會建立源資料庫的備份，並選擇性地複本備份，然後在目標伺服器上將它還原。 當您選取數個資料庫進行遷移時，可能會遇到逾時錯誤。 

從 Data Migration Assistant v2.0 開始，如果您遇到這個問題，您可以減少 parallelDatabases 設定值。 您可以增加此值，以減少整體的遷移時間。

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases="8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>DacFX 設定

在評估期間，Data Migration Assistant 會將資料層應用程式（dacpac）解壓縮，以瞭解資料庫架構。 這種作業可能會因為非常大型的資料庫而失敗，或伺服器是否處於負載中。 從資料移轉 v1.0 開始，您可以修改下列設定值，以避免發生錯誤。 

> [!NOTE]
> 根據預設，整個 &lt;dacfx&gt; 專案會加上批註。 移除批註，然後視需要修改值。

- commandTimeout

   這個參數會設定 IDbCommand. CommandTimeout 屬性 *（以秒為單位）* 。 （預設值 = 60）

- databaseLockTimeout

   這個參數相當於[設定 LOCK\_timeout timeout\_期間](../t-sql/statements/set-lock-timeout-transact-sql.md)（以*毫秒為單位）* 。 （預設值 = 5000）

- maxDataReaderDegreeOfParallelism

  此參數會設定要使用的 SQL 連接集區連接數目。 （預設值 = 8）

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```

## <a name="stretch-database-recommendation-threshold"></a>Stretch Database：建議閾值

使用[SQL Server Stretch Database](https://docs.microsoft.com/sql/sql-server/stretch-database/stretch-database)，您可以將暖和冷交易資料從 Microsoft SQL Server 2016 動態延展到 Azure。 Stretch Database 以具有大量冷資料的交易式資料庫為目標。 [Stretch Database 建議] 下的 [儲存體功能建議] 會先識別其認為將受益于此功能的資料表，然後識別需要進行的變更，才能啟用此功能的資料表。

從 Data Migration Assistant v2.0 開始，您可以使用 recommendedNumberOfRows 設定值來控制資料表的此閾值，以符合 Stretch Database 功能。 預設值為100000個數據列。 如果您想要分析較小的資料表的延展功能，請據以降低值。

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>SQL 連接逾時

藉由將連接逾時值設定為指定的秒數，您可以在執行評量或遷移時，控制來源和目標實例的[SQL 連接逾時](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectiontimeout(v=vs.110).aspx)。 預設值為 15 秒。

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```

## <a name="ignore-error-codes"></a>忽略錯誤代碼

每個規則的標題都有錯誤碼。 如果您不需要規則，而且想要忽略它們，請使用 ignoreErrorCodes 屬性。 您可以指定忽略單一錯誤或多個錯誤。 若要忽略多個錯誤，請使用分號，例如，ignoreErrorCodes = "46010; 71501"。 預設值為71501，這會與物件參考系統物件（例如程式、視圖等）時所識別的未解析參考相關聯。

```
<workflowSettings>

<assessment parallelDatabases="8" ignoreErrorCodes="71501" />

</workflowSettings>
```

## <a name="see-also"></a>另請參閱

[Data Migration Assistant 下載](https://www.microsoft.com/download/details.aspx?id=53595)
