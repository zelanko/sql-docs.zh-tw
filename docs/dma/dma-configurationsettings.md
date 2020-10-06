---
title: 進行 Data Migration Assistant 的設定
description: 瞭解如何藉由更新設定檔中的值來設定 Data Migration Assistant 的設定
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
author: rajeshsetlem
ms.author: rajpo
ms.openlocfilehash: 64c18c32cde0c29c120c8cb1b2d976bd983c774a
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727789"
---
# <a name="configure-settings-for-data-migration-assistant"></a>進行 Data Migration Assistant 的設定

您可以藉由設定 dma.exe.config 檔案中的設定值，微調 Data Migration Assistant 的特定行為。 本文描述重要的設定值。

您可以在電腦的下列資料夾中找到 Data Migration Assistant desktop 應用程式和命令列公用程式的 dma.exe.config 檔案。

- 桌面應用程式

  % ProgramFiles% \\ Microsoft Data Migration Assistant \\dma.exe.config

- 命令列公用程式

  % ProgramFiles% \\ Microsoft Data Migration Assistant \\dmacmd.exe.config 

進行任何修改之前，請務必先儲存原始設定檔的複本。 進行變更之後，請重新開機 Data Migration Assistant，新的設定值才會生效。

## <a name="number-of-databases-to-assess-in-parallel"></a>要以平行方式評估的資料庫數目

Data Migration Assistant 會平行評估多個資料庫。 在評量期間 Data Migration Assistant 將資料層應用程式 (的 dacpac) 解壓縮，以瞭解資料庫架構。如果相同伺服器上的多個資料庫以平行方式進行評估，這項作業可能會有時間。 

從 Data Migration Assistant 2.0 版開始，您可以藉由設定 parallelDatabases 設定值來控制此設定。 預設值為 8。

```
<advisorGroup>

<workflowSettings>

<assessment parallelDatabases="8" />

</workflowSettings>

</advisorGroup>
```




## <a name="number-of-databases-to-migrate-in-parallel"></a>要平行遷移的資料庫數目

Data Migration Assistant 會在遷移登入之前，以平行方式遷移多個資料庫。 在遷移期間，Data Migration Assistant 將會進行源資料庫的備份，並選擇性地複本備份，然後將它還原到目標伺服器上。 選取數個資料庫以進行遷移時，您可能會遇到逾時錯誤。 

從 Data Migration Assistant 2.0 版開始，如果您遇到此問題，您可以減少 parallelDatabases 設定值。 您可以增加此值，以減少整體的遷移時間。

```
<advisorGroup>

<workflowSettings>

<migration parallelDatabases="8″ />

</workflowSettings>

</advisorGroup>
```


## <a name="dacfx-settings"></a>DacFX 設定

在評估期間，Data Migration Assistant 將資料層應用程式 (的 dacpac) 解壓縮，以瞭解資料庫架構。 這項作業可能會因為極大型的資料庫而失敗，或者如果伺服器正在載入，這項作業可能會失敗。 從資料移轉 v1.0 開始，您可以修改下列設定值，以避免發生錯誤。 

> [!NOTE]
> &lt;依預設，整個 dacfx &gt; 專案會加上批註。 移除批註，然後視需要修改值。

- commandTimeout

   此參數會設定 IDbCommand CommandTimeout 屬性（以 *秒為單位）*。 (預設值 = 60) 

- databaseLockTimeout

   此參數相當於 [設定鎖定 \_ 超時 \_ ](../t-sql/statements/set-lock-timeout-transact-sql.md) 時間 *（以毫秒為單位）*。 (預設值 = 5000) 

- maxDataReaderDegreeOfParallelism

  此參數會設定要使用的 SQL 連接集區連接數目。 (預設值 = 8) 

```
<advisorGroup>

<advisorSettings>

<dacFx  commandTimeout="60" databaseLockTimeout="5000"
maxDataReaderDegreeOfParallelism="8"/>

</advisorSettings>

</advisorGroup>
```

## <a name="stretch-database-recommendation-threshold"></a>Stretch Database：建議閾值

您可以使用 [SQL Server Stretch Database](../sql-server/stretch-database/stretch-database.md)，動態地將暖和冷交易資料從 Microsoft SQL Server 2016 延展到 Azure。 Stretch Database 以具有大量冷資料的事務資料庫為目標。 Stretch Database 建議的建議是，在儲存體功能建議下，先識別它認為將會受益于這項功能的資料表，然後識別需要進行的變更，才能啟用這項功能的資料表。

從 Data Migration Assistant 2.0 版開始，您可以使用 recommendedNumberOfRows 設定值來控制資料表的閾值，以符合 Stretch Database 功能。 預設值為100000個數據列。 如果您想要分析偶數個較小資料表的延展功能，請據此將值減少。

```
<advisorGroup>

<advisorSettings>

<stretchDBAdvisor  recommendedNumberOfRows="100000" />

</advisorSettings>

</advisorGroup>
```


## <a name="sql-connection-timeout"></a>SQL 連接逾時

您可以藉由將連接逾時值設定為指定的秒數，在執行評估或遷移時，控制來源和目標實例的 [SQL 連接逾時時間](/dotnet/api/system.data.sqlclient.sqlconnection.connectiontimeout) 。 預設值為 15 秒。

```
<appSettings>

<add key="ConnectionTimeout" value="15" />

</appSettings>
```

## <a name="ignore-error-codes"></a>忽略錯誤碼

每個規則的標題中都有錯誤碼。 如果您不需要規則，而且想要忽略它們，請使用 ignoreErrorCodes 屬性。 您可以指定忽略單一錯誤或多個錯誤。 若要忽略多個錯誤，請使用分號，例如 ignoreErrorCodes = "46010; 71501"。 預設值為71501，與物件參考系統物件（如程式、視圖等）時所識別的無法解析參考相關聯。

```
<workflowSettings>

<assessment parallelDatabases="8" ignoreErrorCodes="71501" />

</workflowSettings>
```

## <a name="see-also"></a>另請參閱

[Data Migration Assistant 下載](https://www.microsoft.com/download/details.aspx?id=53595)