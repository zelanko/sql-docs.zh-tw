---
title: 使用 cron 排程 Linux 上的 SSIS 套件
description: 本文描述如何使用 cron 服務排程 Linux 上的 SQL Server Integration Services (SSIS) 套件。
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ac7648287b4e4b609f4dd4f25b1b07a512065364
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68065166"
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>使用 cron 排程 Linux 上的 SQL Server Integration Services 套件執行

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

當您在 Windows 上執行 SQL Server Integration Services (SSIS) 和 SQL Server 時，可以使用 SQL Server Agent 自動執行 SSIS 套件。 不過，當您在 Linux 上執行 SQL Server 和 SSIS 時，SQL Server Agent 公用程式無法在 Linux 上排程作業。 因此，您可以改用在 Linux 平台上廣泛使用的 cron 服務來自動執行套件。

本文提供的範例會示範如何自動執行 SSIS 套件。 這些範例是針對在 Red Hat Enterprise 上執行所撰寫。 若要用於其他 Linux 發行版本 (例如 Ubuntu)，可採用類似的程式碼。

## <a name="prerequisites"></a>Prerequisites

使用 cron 服務執行作業之前，請先檢查您的電腦是否正在執行 cron 服務。

若要檢查 cron 服務的狀態，請使用下列命令：`systemctl status crond.service`。

如果服務並不在作用中狀態 (也就是未執行)，請洽詢您的系統管理員以正確設定 cron 服務。

## <a name="create-jobs"></a>建立作業

cron 作業是一項可以設定為以指定間隔定期執行的工作。 此作業可以非常簡單，就像您直接在主控台中鍵入或以殼層指令碼形式執行的命令一般。

為了方便管理和維護，建議您將套件執行命令放在包含描述性名稱的指令碼中。

以下是執行套件的簡單殼層指令碼範例。 它只包含一個命令，但您可以視需要新增更多命令。

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>使用 cron 服務排程作業

定義您的作業之後，您可以使用 cron 服務將其排程為自動執行。

若要新增由 cron 執行的作業，請在 crontab 檔案中新增作業。 若要在編輯器中開啟 crontab 檔案以新增或更新作業，請使用下列命令：`crontab -e`。

若要將先前所述的作業排定在每天上午 2:10 執行，請將下行新增至 crontab 檔案：

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

儲存 crontab 檔案，然後結束編輯器。

若要了解範例命令的格式，請檢閱下一節中的資訊。
 
## <a name="format-of-a-crontab-file"></a>crontab 檔案的格式

下圖顯示新增至 crontab 檔案的作業行格式描述。

![crontab 檔案中的項目格式描述](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

若要取得 crontab 檔案格式的詳細描述，請使用下列命令：`man 5 crontab`。

以下是輸出的部分範例，其有助於說明本文中的範例：

![crontab 格式的詳細部分描述](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>Linux 上的 SSIS 相關內容
-   [使用 SSIS 在 Linux 上擷取、轉換和載入資料](sql-server-linux-migrate-ssis.md)
-   [在 Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [使用 ssis-conf 設定 Linux 上的 SQL Server Integration Services](sql-server-linux-configure-ssis.md)
-   [Linux 上的 SSIS 限制和已知問題](sql-server-linux-ssis-known-issues.md)
