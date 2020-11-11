---
title: 在已啟用 Azure Arc 的 SQL Server 執行個體上設定隨選 SQL 評定
description: 在已啟用 Azure Arc 的 SQL Server 執行個體上設定隨選 SQL 評定
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: c6f2a0989cb13253ef4a6a26e013a6b8c7a84ded
ms.sourcegitcommit: f888ac94c7b5f6b6f138ab75719dadca04e8284a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93294382"
---
# <a name="configure-sql-assessment-on-an-azure-arc-enabled-sql-server-instance"></a>在已啟用 Azure Arc 的 SQL Server 執行個體上設定 SQL 評定

SQL 評定會提供機制供您評估 SQL Server 的設定。 本文提供在已啟用 Azure Arc 的 SQL Server 執行個體上使用 SQL 評定的指示。

## <a name="prerequisites"></a>Prerequisites

* 您的 SQL Server 執行個體必須連線到 Azure Arc。如需指示，請參閱[將 SQL Server 連線到 Azure Arc](connect.md) 一文。

* Microsoft Monitoring Agent (MMA) 擴充功能必須已安裝在電腦上並完成設定。 如需指示，請檢視[安裝 MMA](configure-advanced-data-security.md#install-microsoft-monitoring-agent-mma) 一文。 您也可以在 [Log Analytics 代理程式](/azure/azure-monitor/platform/log-analytics-agent)一文上取得詳細資訊。

* 您的 SQL Server 執行個體必須[啟用 TCP/IP 通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。

* [SQL Server 瀏覽器服務](../../tools/configuration-manager/sql-server-browser-service.md)必須正在執行中 (如果您要操作 SQL Server 的具名執行個體)。

* 請確定您已檢閱[服務中樞隨選評定必要條件](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents)上的 SQL Server 文件。

## <a name="run-on-demand-sql-assessment"></a>執行隨選 SQL 評定

1. 開啟您的 SQL Server – Azure Arc 資源，然後選取左側窗格中的 [環境健康情況]。

   > [!div class="mx-imgBorder"]
   > [ ![螢幕擷取畫面，顯示 SQL Server - Azure Arc 資源的環境健康情況畫面。](media/assess/sql-assessment-heading-sql-server-arc.png) ](media/assess/sql-assessment-heading-sql-server-arc.png#lightbox)

> [!IMPORTANT]
> 如果未安裝 MMA 延伸模組，您將無法起始隨選 SQL 評定。

2. 選取帳戶類型。 如果您有受控服務帳戶，則其可讓您直接從入口網站起始 SQL 評定。 請指定帳戶名稱。

> [!NOTE]
> 指定「受控的服務帳戶」會啟用 [Configure SQL Assessment] \(設定 SQL 評定\) 按鈕，讓您可藉由部署 *CustomScriptExtension* ，以從入口網站起始評定。 因為一次只能部署一個 *CustomScriptExtension* ，所以執行後會自動移除 SQL 評定的指令碼延伸模組。 如果已將另一個 *CustomScriptExtension* 部署到主機電腦，則不會啟用 [Configure SQL Assessment] \(設定 SQL 評定\) 按鈕。

3. 如果想要變更預設值，請指定資料收集電腦上的工作目錄。 預設會使用 `C:\sql_assessment\work_dir`。 在收集和分析期間，資料會暫時儲存在該資料夾中。 如果資料夾不存在，則會自動建立。

4. 如果按一下 [Configure SQL Assessment] \(設定 SQL 評定\) 從入口網站起始 SQL 評定，則會顯示標準部署泡泡。

> [!div class="mx-imgBorder"]
   > [ ![顯示 CustomScriptExtension 部署的螢幕擷取畫面。](media/assess/sql-assessment-custom-script-deployment.png) ](media/assess/sql-assessment-custom-script-deployment.png#lightbox)

5. 如果想要從目標電腦起始 SQL 評定，請按一下 [下載組態指令碼]，將下載的指令碼複製到目標電腦，然後在 **powershell.exe** 的管理執行個體中執行下列其中一個程式碼區塊：

   * _網域帳戶_ ：系統會提示您輸入使用者帳戶和密碼。

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1'
      ```

   * _受控服務帳戶 (MSA)_

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1' -ManagedServiceAccountName <MSA account name>
      ```

> [!NOTE]
> 指令碼會排程名為 *SQLAssessment* 的工作，以觸發資料收集。 此工作會在您執行指令碼後的一小時內執行。 然後每隔七天重複執行一次。

> [!TIP]
> 您可將工作修改為在不同的日期和時間執行，或甚至強制其立即執行。 在工作排程器程式庫中，尋找 [Microsoft] > [Operations Management Suite] > [AOI] **\*\*\***  > [評定] > [SQLAssessment]。

## <a name="view-sql-assessment-results"></a>檢視 SQL 評定結果

* 在 [環境健康情況] 窗格中，選取 [檢視 SQL 評定結果] 按鈕。

   > [!NOTE]
   > [檢視 SQL 評定結果] 按鈕會保持停用狀態，直到 Log Analytics 中的結果就緒為止。 目標電腦處理資料檔案後，此流程可能需要最多兩個小時的時間。

   > [!div class="mx-imgBorder"]
   > [ ![顯示 SQL 評定結果的螢幕擷取畫面。](media/assess/sql-assessment-results.png) ](media/assess/sql-assessment-results.png#lightbox)

* 您可以藉由查看工作資料夾中的檔案，來確認集合機器上的資料處理狀態。 排定的工作完成後，您應該會在工作目錄中看到數個具有 _new._ 前置詞的檔案。

   > [!div class="mx-imgBorder"]
   > [ ![螢幕擷取畫面：顯示 [檔案管理員] 視窗，其中顯示工作資料夾中的新資料檔案。](media/assess/sql-assessment-data-files-ready.png) ](media/assess/sql-assessment-data-files-ready.png#lightbox)

* Microsoft Monitoring Agent 會每隔 15 分鐘掃描工作資料夾一次。 其會尋找 _new.*_ 檔案，並將資料傳送至 Log Analytics 工作區。 在 MMA 上傳檔案之後，其會將前置詞從 _new._ 變更為 _processed._

   > [!div class="mx-imgBorder"]
   > ![螢幕擷取畫面：顯示 [檔案管理員] 視窗，其中顯示已處理的資料檔案。](media/assess/sql-assessment-data-files-processed.png)

## <a name="next-steps"></a>後續步驟

* 若要取得詳細資訊，請檢視[服務中樞隨選評定](/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents)上的必要條件文件。

* 若要取得隨選 SQL 評定功能的完整支援，您必須有頂級或統一的支援訂用帳戶。 如需詳細資訊，請參閱 [Azure 頂級支援](https://azure.microsoft.com/support/plans/premier)。
