---
title: "排程在 Linux 上的 SSIS 封裝與 cron |Microsoft 文件"
description: "這篇文章描述如何排程在 Linux 上的 cron 服務的 SQL Server Integration Services (SSIS) 封裝。"
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 84ee0eaf4743cc4a3b188dd700b1ccbdc4ca42cc
ms.contentlocale: zh-tw
ms.lasthandoff: 10/10/2017

---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>排程 SQL Server Integration Services 封裝執行 Linux 上的 cron

當您在 Windows 上執行 SQL Server Integration Services (SSIS) 和 SQL Server 時，您可以使用 SQL Server Agent 自動化 SSIS 封裝的執行。 當您在 Linux 上執行 SQL Server 和 SSIS 時，不過，SQL Server 代理程式公用程式無法排程在 Linux 上的作業。 相反地，您可以使用自動化封裝執行廣泛使用在 Linux 平台的 cron 服務。

這篇文章會提供示範如何讓 SSIS 封裝執行自動化的範例。 範例會在 Red Hat Enterprise 上執行寫入。 針對其他 Linux 發行版本，例如 Ubuntu 相似的程式碼。

## <a name="prerequisites"></a>必要條件

使用 cron 服務執行作業之前，請檢查是否正在執行您的電腦上。

若要檢查 cron 服務的狀態，請使用下列命令： `systemctl status crond.service`。

如果服務不在作用中 （也就未執行），請參閱您的系統管理員安裝及正確設定 cron 服務。

## <a name="create-jobs"></a>建立作業

Cron 作業是您可以設定定期依指定的間隔執行的工作。 作業可以做為命令，通常會直接在主控台中輸入或執行身分的殼層指令碼一樣簡單。

容易管理和維護的用途，我們建議您將封裝執行命令放在指令碼中包含的描述性名稱。

以下是簡單的殼層指令碼來執行封裝的範例。 它包含只單一命令，但您可以視需要新增更多的命令。

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Cron 服務與排程工作

定義您的工作之後，您可以排程自動執行，藉由使用 cron 服務。

若要新增您要執行的 cron 作業，加入 crontab 檔案中的作業。 若要開啟 crontab 檔案中的編輯器，您可以在其中新增或更新作業，請使用下列命令： `crontab -e`。

若要排程每日在上午 2:10 執行先前所述的工作，將下列行加入 crontab 檔案：

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

儲存 crontab 檔案，並再結束編輯器。

若要了解範例命令的格式，請檢閱下列章節中的資訊。
 
## <a name="format-of-a-crontab-file"></a>Crontab 檔案格式

下圖顯示工作列加入至 crontab 檔案的格式化描述。

![格式描述 crontab 檔案中的項目](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

若要取得 crontab 檔案格式的更詳細的描述，請使用下列命令： `man 5 crontab`。

以下是部分的範例，可協助說明本文章中的範例的輸出：

![詳細的說明部分 crontab 格式](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

