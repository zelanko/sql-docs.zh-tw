---
title: 為已啟用 Azure Arc 的 SQL Server 設定 SQL 評定
titleSuffix: ''
description: 為已啟用 Azure Arc 的 SQL Server 執行個體設定隨選評定
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 41a7f1f4edc247f211ee5b3cdcaddfd139c5027c
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988014"
---
# <a name="configure-on-demand-sql-assessment-for-azure-arc-enabled-sql-server-instance"></a>為已啟用 Azure Arc 的 SQL Server 執行個體設定 SQL 評定

您可以依照下列步驟，為您的 SQL Server 執行個體啟用 SQL 評定。

## <a name="prerequisites"></a>必要條件

* 您的 SQL Server 執行個體已連線至 Azure Arc。依照這些指示，[將 SQL Server 執行個體上線至已啟用 Arc 的 SQL Server](connect.md)。

* 在機器上安裝並設定 MMA 延伸模組。 依照這些指示[安裝 Microsoft Monitoring Agent (MMA)](configure-advanced-data-security.md#install-microsoft-monitoring-agent-mma)。 如需詳細資訊，請參閱 [Log Analytics 代理程式](/azure/azure-monitor/platform/log-analytics-agent)。

* 您的 SQL Server [已啟用 TCP/IP 通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。

* [SQL Server 瀏覽器](../../tools/configuration-manager/sql-server-browser-service.md)正在執行中 (如果您要操作 SQL Server 的具名執行個體)。

* 您已檢閱[服務中樞隨選評定必要條件](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents)上的 SQL Server 文件。

## <a name="enable-on-demand-sql-assessment"></a>啟用隨選 SQL 評定

1. 開啟您的 SQL Server – Azure Arc 資源，然後選取左側功能表中的 [環境健康情況]。

   ![SQL 評定選取](media/assess/sql-assessment-heading-sql-server-arc.png)

1. 指定資料收集機器上的工作目錄。 根據預設，將會使用 `C:\sql_assessment\work_dir`。 在收集和分析期間，資料會暫時儲存在該資料夾底下。 如果資料夾不存在，則會自動建立。

1. 按一下 [下載設定指令碼]，然後將下載的指令碼複製到目標機器。

1. 啟動 __powershell.exe__ 的系統管理執行個體，然後執行下列其中一項： 
   * 如果您使用網域帳戶，請執行下列命令。 系統會提示您輸入使用者帳戶和密碼。 

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1'
      ```

    * 如果您使用 MSA 帳戶，請執行下列命令。

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1' -ManagedServiceAccountName <MSA account name>
      ```

   > [!NOTE]
   > 指令碼會排程名為 *SQLAssessment* 的工作，使其在執行前一個指令碼後的一小時內執行，然後每 7 天執行一次。 此工作可修改成在不同的日期和時間執行，甚或從工作排程器程式庫 > Microsoft > Operations Management Suite > AOI*** > 評定 > SQLAssessment 強制立即執行。 此工作會觸發資料收集。

## <a name="view-the-assessment-results"></a>檢視評定結果

[環境健康情況] 刀鋒視窗上的 [檢視 SQL 評定結果] 按鈕會停用，直到 Log Analytics 中的結果準備就緒為止。 按鈕啟用後，只要按一下即可檢視結果。 在目標機器上處理資料檔案之後，最多可能需要 2 小時才能在 Log Analytics 中看到結果。

![SQL 評定結果](media/assess/sql-assessment-results.png)

您可以藉由查看工作資料夾中的檔案，來確認集合機器上的資料處理狀態。 排定的工作完成後，您應該會在工作目錄中看到數個具有 _new._ 前置詞的檔案：

![資料檔案就緒](media/assess/sql-assessment-data-files-ready.png)

Microsoft Monitoring Agent 會每 15 分鐘掃描工作資料夾一次，以尋找 _new.*_ 檔案，然後將資料傳送至 Log analytics 工作區。 檔案上傳之後，前置詞就會從 _new._ 變更 為 _processed._ ：

![已處理資料檔案](media/assess/sql-assessment-data-files-processed.png)

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱[服務中樞隨選評定必要條件](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents)中的 SQL Server 文件。

若要取得隨選 SQL 評定的完整支援，需要頂級或統一的支援訂用帳戶。 如需詳細資訊，請參閱 [Azure 頂級支援](https://azure.microsoft.com/support/plans/premier)。