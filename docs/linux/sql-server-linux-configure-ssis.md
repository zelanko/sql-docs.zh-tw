---
title: "使用 ssis conf，設定 Linux 上的 SSIS |Microsoft 文件"
description: "本文示範如何在 Linux 上設定 SQL Server Integration Services，ssis conf 公用程式。"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 09/26/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: integration-services
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 46327772e8c22f76770bc51f72817ceedffae469
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>使用 ssis conf，設定 Linux 上的 SQL Server Integration Services

`ssis-conf`組態指令碼時，您安裝 SQL Server Integration Services (SSIS) Red Hat Enterprise Linux 和 Ubuntu。 您可以使用此公用程式來設定下列屬性：

| Command | Description |
|-------------|---------------------------------------------------------------------|
| set 版本 | 設定版本的 SQL Server                                       |
| 遙測   | 啟用或停用 SQL Server Integration Services 遙測服務 |
| 安裝程式       | 初始化和設定 Microsoft SQL Server Integration Services      |
|||

## <a name="how-to-run-ssis-conf"></a>如何執行 ssis conf

執行這份文件中的範例`ssis-conf`藉由指定完整路徑： `/opt/ssis/bin/ssis-conf`。 如果在執行之前，您導覽至該路徑`ssis-conf`，您可以在目前目錄的內容中執行此公用程式： `./ssis-conf`。

請確定您執行與根權限的這篇文章所述的命令。 例如，執行`sudo /opt/ssis/bin/ssis-conf setup`而非`/opt/ssis/bin/ssis-conf setup`。

若要執行這些命令提示，以您偏好的語言，您可以指定地區設定。 例如，若要查看中文的提示，請執行下列命令：

`sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`。

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>使用組版本設定的 SQL Server Integration Services 版本

對齊的 SSIS 版本的 SQL Server 版本。

輸入下列命令：

`$ sudo /opt/ssis/bin/ssis-conf set-edition`

您輸入命令之後，您會看到下列提示：

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

Details about editions can be found at

https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409

Use of PAID editions of this software requires separate licensing through a

Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate

number of licenses in place to install and run this software.

Enter your edition(1-8):
```

如果輸入介於 1 到 7 之間的值，則系統會設定為免費或付費版本。 如果您輸入 8 時，此公用程式會提示您輸入您購買的產品金鑰：

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>使用遙測技術來設定客戶意見反應

`telemetry`命令會判斷是否 SSIS 傳送意見給 Microsoft。

可用的版本 （也就是 Express、 Developer 和 Evaluation 版本），一定會啟用遙測服務。 如果您有免費版本，您無法使用`telemetry`命令以停用遙測。

輸入下列命令：

`$ sudo /opt/ssis/bin/ssis-conf telemetry`

對於付費版本，您輸入命令之後, 您會看到下列提示：

```
Send feature usage data to Microsoft. Feature usage data includes information
about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

如果選擇**是**，遙測服務已啟用並開始執行。 服務自動啟動後每個開機。 如果選擇**否**，遙測服務停止，並已停用。

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>使用安裝程式初始化與設定 Microsoft SQL Server Integration Services

使用`setup`命令每次您安裝 SSIS。

輸入下列命令：

`sudo /opt/ssis/bin/ssis-conf setup`

此公用程式會提示您確認，或提供下列項目中的值：
-   產品授權
-   使用者授權合約
-   遙測服務
-   Integration Services 所使用的語言

若要執行`setup`命令提示字元的語言，您希望，您可以指定地區設定。 例如，若要查看中文的提示，執行下列命令： `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`。

## <a name="ssisconf-format"></a>ssis.conf 格式

下列`/var/opt/ssis/ssis.conf`每個設定檔提供的範例。

針對 SQL Server，您可以變更系統設定中的值來`mssql.conf`檔案。 Ssis，您**無法**中的值來變更系統設定`ssis.conf`檔案。 `ssis.conf`檔案只會顯示安裝程式的結果。 如果您想要變更適用於 SSIS 的設定，您可以刪除`ssis.conf`檔，然後執行`setup`命令一次。

以下是範例`ssis.conf`檔案。 每個欄位對應至一個安裝程式步驟的結果。

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
