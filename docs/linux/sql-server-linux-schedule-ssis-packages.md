---
title: 在 Linux 上使用 cron 的排程 SSIS 套件
description: 這篇文章描述如何排程的 cron 服務在 Linux 上的 SQL Server Integration Services (SSIS) 套件。
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ac7648287b4e4b609f4dd4f25b1b07a512065364
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065166"
---
# <a name="schedule-sql-server-integration-services-package-execution-on-linux-with-cron"></a>排程 SQL Server Integration Services 封裝執行在 Linux 上的使用 cron

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

當您在 Windows 上執行 SQL Server Integration Services (SSIS) 和 SQL Server 時，您可以使用 SQL Server Agent 自動化中的執行 SSIS 套件。 當您在 Linux 上執行 SQL Server 和 SSIS 時，不過，SQL Server 代理程式公用程式無法用來排程 Linux 上的作業。 相反地，您可以使用廣泛用來讓封裝執行自動化的 Linux 平台的 cron 服務。

本文提供範例，示範如何自動執行的 SSIS 套件。 範例會寫入至 Red Hat Enterprise 上執行。 程式碼很類似 Linux 散發套件，例如 Ubuntu 的項目。

## <a name="prerequisites"></a>先決條件

執行作業的情況下，您在使用 cron 服務之前，請檢查以查看它是否您的電腦上執行。

若要檢查 cron 服務的狀態，請使用下列命令： `systemctl status crond.service`。

如果服務不在使用中 （也就未執行），請參閱您的系統管理員安裝及正確設定 cron 服務。

## <a name="create-jobs"></a>建立作業

Cron 作業是您可以設定為指定的間隔定期執行的工作。 作業可以是簡單，只要您通常可以直接在主控台中輸入，或殼層指令碼以執行的命令。

讓您輕鬆管理和維護的用途，我們建議您執行封裝的命令置於包含的描述性名稱的指令碼。

以下是簡單的殼層指令碼來執行封裝的範例。 它包含只單一命令，但您可以視需要新增更多命令。

```bash
# A simple shell script that contains a simple package execution command
# Script name: SSISpackageName.daily

/opt/ssis/bin/dtexec /F yourSSISpackageName.dtsx >> $HOME/tmp/out 2>&1
```

## <a name="schedule-jobs-with-the-cron-service"></a>Cron 服務的排程工作

定義您的工作之後，您可以排程自動執行使用 cron 服務。

若要新增您的 cron 來執行的作業，請在 crontab 檔加入作業。 若要開啟的編輯器，您可以在其中新增或更新作業 crontab 檔案，請使用下列命令： `crontab -e`。

若要排程每日上午 2:10 點執行先前所述的工作，請將下行新增到 crontab 檔案：

```
# run <SSIS package name> at 2:10 AM every day
10 2 \* \* \* $/HOME/SSIS/jobs/SSISpackageName.daily
```

儲存系統檔案，然後再結束編輯器。

若要了解範例命令的格式，請檢閱下一節中的資訊。
 
## <a name="format-of-a-crontab-file"></a>Crontab 檔案格式

下圖顯示工作列新增到 crontab 檔案的格式為： 描述。

![格式為： 描述 crontab 檔案中的項目](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-job-definition.png)

若要取得 crontab 檔案格式的更詳細的描述，請使用下列命令： `man 5 crontab`。

以下是部分的範例，協助說明本文中的範例的輸出：

![詳細的說明部分 crontab 格式](media/sql-server-linux-schedule-ssis-packages/ssis-linux-cron-crontab-format.png)

## <a name="related-content-about-ssis-on-linux"></a>關於 Linux 上的 SSIS 的相關的內容
-   [擷取、 轉換和載入與 SSIS Linux 上的資料](sql-server-linux-migrate-ssis.md)
-   [在 Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [在 Linux 上設定 SQL Server Integration Services 使用 ssis conf](sql-server-linux-configure-ssis.md)
-   [限制與已知的問題適用於 Linux 上的 SSIS](sql-server-linux-ssis-known-issues.md)
