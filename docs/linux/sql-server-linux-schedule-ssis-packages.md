---
title: "排程在 Linux 上的 SSIS 封裝與 cron |Microsoft 文件"
description: "這篇文章會示範如何排程在 Linux 上的 cron 服務的 SQL Server Integration Services 封裝。"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 09/26/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 31d5fb63a9c2a4d8825aa39c6fa7e3377ddc8d91
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>排程 SQL Server Integration Services 封裝執行 Linux 上的 cron

當您在 Windows 上執行 SQL Server Integration Services (SSIS) 和 SQL Server 時，您可以使用 SQL Server Agent 自動化 SSIS 封裝的執行。 當您在 Linux 上執行 SQL Server 和 SSIS 時，不過，SQL Server 代理程式公用程式無法排程在 Linux 上的作業。 改為使用**Cron**廣泛使用自動化封裝執行的 Linux 平台的服務。

這篇文章會提供示範如何讓 SSIS 封裝執行自動化的範例。 Red Hat Enterprise 上執行所撰寫的範例。 針對其他 Linux 散發套件，例如 Ubuntu 相似的程式碼。

## <a name="prerequisites"></a>必要條件

您可以使用 Cron 服務來執行作業之前，您必須檢查 Cron 服務是否正在執行您的電腦上。

使用下列命令來檢查 Cron 服務的狀態。

`systemctl status crond.service`

如果服務不在作用中 （也就是，未執行），請參閱您的系統管理員安裝及正確設定 Cron 服務。

## <a name="create-jobs"></a>建立作業

Cron 作業是您可以設定定期依指定的間隔執行的工作。 作業可以做為命令，通常會直接在主控台中輸入或執行身分的殼層指令碼一樣簡單。

容易管理和維護的用途，建議您將封裝的執行命令放到指令碼中使用描述性的名稱。

以下是包含只有單一命令，以執行封裝的殼層指令碼的簡單範例。 您可以視需要新增更多的命令。

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Cron 服務與排程工作

定義您的工作之後，您可以排程自動執行，藉由使用 Cron 服務。

若要新增您要執行的 Cron 作業，您必須加入作業中的`crontab`檔案。 若要開啟`crontab`檔案在編輯器中您可以在其中新增或更新作業，請使用下列命令：

`crontab -e`

若要排程在每天上午 2:10 執行先前所述的工作，加上下列列`crontab`檔案：

```
# run SSIS package Name at 2:10AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

儲存`crontab`檔案並結束編輯器。

若要了解範例命令的格式，請檢閱下列章節中的資訊。
 
## <a name="format-of-a-crontab-file"></a>Crontab 檔案格式

下圖顯示加入至工作行的格式描述`crontab`檔案。

![格式描述 crontab 檔案中的項目](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

若要取得更詳細的描述`crontab`檔案格式，請使用下列命令：

`man 5 crontab`

以下是部分的範例，可協助說明本文章中的範例的輸出：

![詳細的說明部分 crontab 格式](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

