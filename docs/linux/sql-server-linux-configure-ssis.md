---
title: 在 Linux 上設定 SSIS 以 ssis conf |Microsoft Docs
description: 本文說明如何使用 ssis conf 公用程式在 Linux 上設定 SQL Server Integration Services (SSIS)。
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 22662a8e4212d0856501a888efed05e35d372ac5
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084320"
---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>在 Linux 上設定 SQL Server Integration Services 使用 ssis conf

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

在您執行`ssis-conf`Red Hat Enterprise Linux 和 Ubuntu 安裝 SQL Server Integration Services (SSIS) 時的設定指令碼。 如需安裝 SSIS 的詳細資訊，請參閱[安裝 SQL Server Integration Services (SSIS) 在 Linux 上](sql-server-linux-setup-ssis.md)。

您也可以使用`ssis-conf`公用程式來設定下列屬性：

| 命令 | 描述 |
|-------------|---------------------------------------------------------------------|
| 設定版本 | 設定 SQL Server 的版本                                       |
| 遙測   | 啟用或停用 SQL Server Integration Services 遙測服務 |
| 安裝程式       | 初始化和設定 Microsoft SQL Server Integration Services      |
|||

## <a name="run-ssis-conf"></a>執行 ssis conf

執行這篇文章中的範例`ssis-conf`藉由指定完整路徑： `/opt/ssis/bin/ssis-conf`。 如果您瀏覽至該位置執行之前`ssis-conf`，您可以在目前目錄的內容中執行此公用程式： `./ssis-conf`。

請務必在執行中以根權限的這篇文章所述的命令。 例如，執行`sudo /opt/ssis/bin/ssis-conf setup`而非`/opt/ssis/bin/ssis-conf setup`。

若要執行這些命令提示在您偏好的語言中，您可以指定地區設定。 例如，若要以中文收到提示，請執行下列命令： `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`。

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>若要設定的 SQL Server Integration Services 版本使用組版本

SSIS 的版本與版本的 SQL Server 對齊。

輸入下列命令： `$ sudo /opt/ssis/bin/ssis-conf set-edition`。

您輸入命令之後，您會收到下列提示：

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

如果您輸入的值從 1 到 7，系統就會設定為免費或付費版。 如果您輸入 8 時，此公用程式會提示您輸入您購買的產品金鑰：

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>使用遙測來設定客戶的意見反應

`telemetry`命令會判斷是否 SSIS 會將意見反應傳送給 Microsoft。

適用於免費版本 （也就是快速、 Developer 和 Evaluation 版本），一律會啟用遙測服務。 如果您有免費版本，您無法使用`telemetry`命令來停用遙測。

輸入下列命令： `$ sudo /opt/ssis/bin/ssis-conf telemetry`。

付費版本，您輸入命令之後, 您會收到下列提示：

```
Send feature usage data to Microsoft. Feature usage data includes information about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

如果您選取**是**，遙測服務已啟用，並開始執行。 每個開機之後自動啟動服務。 如果您選取**No**，遙測服務會停止，並已停用。

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>使用安裝程式初始化和設定 Microsoft SQL Server Integration Services

使用`setup`命令每次您安裝 SSIS。

輸入下列命令： `sudo /opt/ssis/bin/ssis-conf setup`。

此公用程式會提示您確認，或提供下列項目中的值：
-   產品授權
-   使用者授權合約
-   遙測服務
-   Integration Services 所使用的語言

若要執行`setup`命令和在語言中的提示，您希望，您可以指定地區設定。 例如，若要以中文收到提示，請執行下列命令： `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`。

## <a name="ssisconf-format"></a>ssis.conf 格式

下列`/var/opt/ssis/ssis.conf`檔案提供每個設定的範例。

針對 SQL Server，您可以變更系統設定中的值的變化`mssql.conf`檔案。 適用於 SSIS，您*無法*藉由變更中的值變更系統設定`ssis.conf`檔案。 `ssis.conf`檔案會顯示安裝程式的結果。 如果您想要變更適用於 SSIS 的設定，您可以刪除`ssis.conf`檔案，並執行`setup`命令一次。

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

## <a name="related-content-about-ssis-on-linux"></a>關於 Linux 上的 SSIS 的相關的內容
-   [擷取、 轉換和載入與 SSIS Linux 上的資料](sql-server-linux-migrate-ssis.md)
-   [在 Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [限制與已知的問題適用於 Linux 上的 SSIS](sql-server-linux-ssis-known-issues.md)
-   [排程 SQL Server Integration Services 封裝執行在 Linux 上的使用 cron](sql-server-linux-schedule-ssis-packages.md)
