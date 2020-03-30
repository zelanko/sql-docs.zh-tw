---
title: 使用 ssis-conf 設定 Linux 上的 SSIS
description: 本文描述如何使用 ssis-conf 公用程式設定 Linux 上的 SQL Server Integration Services (SSIS)。
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 51dc2ba27e346dea75f1bd347491d4932695fd43
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68077527"
---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>使用 ssis-conf 設定 Linux 上的 SQL Server Integration Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

當您安裝適用於 Red Hat Enterprise Linux 和 Ubuntu 的 SQL Server Integration Services (SSIS) 時，您將執行 `ssis-conf` 設定指令碼。 如需安裝 SSIS 的詳細資訊，請參閱[在 Linux上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)。

您也可以使用 `ssis-conf` 公用程式來設定下列屬性：

| Command | 描述 |
|-------------|---------------------------------------------------------------------|
| set-edition | 設定 SQL Server 的版本                                       |
| 遙測   | 啟用或停用 SQL Server Integration Services 遙測服務 |
| 安裝程式       | 初始化和設定 Microsoft SQL Server Integration Services      |
|||

## <a name="run-ssis-conf"></a>執行 ssis-conf

本文中的範例是藉由指定完整路徑：`ssis-conf` 來執行 `/opt/ssis/bin/ssis-conf`。 如果您在執行 `ssis-conf` 之前巡覽至該位置，則您可以在目前目錄的內容中執行公用程式：`./ssis-conf`。

請務必使用根權限來執行本文中所述命令。 例如，執行 `sudo /opt/ssis/bin/ssis-conf setup` 而不是 `/opt/ssis/bin/ssis-conf setup`。

若要使用您偏好的語言提示來執行這些命令，您可以指定地區設定。 例如，若要以中文接收提示，請執行下列命令：`sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`。

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>使用 set-edition 來設定 SQL Server Integration Services 的版本

SSIS 版本與 SQL Server 的版本一致。

輸入下列命令：`$ sudo /opt/ssis/bin/ssis-conf set-edition`。

輸入命令之後，您會收到下列提示：

```
Choose an edition of SQL Server:

1) Evaluation (free, no production use rights, 180-day limit)

2) Developer (free, no production use rights)

3) Express (free)

4) Web (PAID)

5) Standard (PAID)

6) Enterprise (PAID)

7) Enterprise Core (PAID)

8) I bought a license through a retail sales channel and have a product key to enter.

Details about editions can be found at https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409.

Use of PAID editions of this software requires separate licensing through a Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate number of licenses in place to install and run this software.

Enter your edition (1-8):
```

如果您輸入 1 到 7 的值，系統會設定免費或付費版本。 如果您輸入 8，公用程式會提示您輸入您購買的產品金鑰：

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>使用遙測來設定客戶意見反應

`telemetry` 命令會判斷 SSIS 是否要將意見反應傳送給 Microsoft。

針對免費版本 (也就是 Express、Developer 和評估版)，遙測服務一律為啟用。 如果您有免費版本，則無法使用 `telemetry` 命令來停用遙測。

輸入下列命令：`$ sudo /opt/ssis/bin/ssis-conf telemetry`。

針對付費版本，在輸入命令之後，您會收到下列提示：

```
Send feature usage data to Microsoft. Feature usage data includes information about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

如果您選取 [是]  ，遙測服務即會啟用並開始執行。 服務會在每次開機後自動啟動。 如果您選取 [否]  ，遙測服務即會停止並停用。

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>使用安裝程式來初始化及設定 Microsoft SQL Server Integration Services

您每次安裝 SSIS 時，請使用 `setup` 命令。

輸入下列命令：`sudo /opt/ssis/bin/ssis-conf setup`。

公用程式會提示您確認或提供下列項目的值：
-   產品授權
-   EULA 合約
-   遙測服務
-   Integration Services 所使用的語言

若要使用您偏好的語言提示來執行 `setup` 命令，您可以指定地區設定。 例如，若要以中文接收提示，請執行下列命令：`sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`。

## <a name="ssisconf-format"></a>ssis.conf format

下列 `/var/opt/ssis/ssis.conf` 檔案提供每項設定的範例。

針對 SQL Server，您可以藉由變更 `mssql.conf` 檔案中的值來變更系統設定。 針對 SSIS，您「無法」  藉由變更 `ssis.conf` 檔案中的值來變更系統設定。 `ssis.conf` 檔案只會顯示安裝程式的結果。 如果您希望變更 SSIS 的設定，可以刪除 `ssis.conf` 檔案，然後再次執行 `setup` 命令。

以下是範例 `ssis.conf` 檔案。 每個欄位都對應至一個設定步驟的結果。

```
[LICENSE]
                       
registered = Y        
                       
pid = enterprisecore  
                       
[EULA]
                       
accepteula = Y        
                       
[TELEMETRY]
                       
enabled = Y           
                       
[language]
                       
lcid = 2052
```

## <a name="related-content-about-ssis-on-linux"></a>Linux 上的 SSIS 相關內容
-   [使用 SSIS 在 Linux 上擷取、轉換和載入資料](sql-server-linux-migrate-ssis.md)
-   [在 Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [Linux 上的 SSIS 限制和已知問題](sql-server-linux-ssis-known-issues.md)
-   [使用 cron 排程 Linux 上的 SQL Server Integration Services 套件執行](sql-server-linux-schedule-ssis-packages.md)
