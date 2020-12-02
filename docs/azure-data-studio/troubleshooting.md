---
title: 針對 Azure Data Studio 進行疑難排解
description: 了解如何取得記錄並針對 Azure Data Studio 進行疑難排解，這樣將有助回報錯誤 (Bug) 報表。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: hanqin, maghan
ms.custom: seodec18
ms.date: 11/24/2020
ms.openlocfilehash: 1d2483532589cd840f1120cfb0ac3273b41e0bb5
ms.sourcegitcommit: 2e7154475ba1f31d1aeebc8f48ac05846f793736
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "95920206"
---
# <a name="azure-data-studio-troubleshooting"></a>針對 Azure Data Studio 進行疑難排解
Azure Data Studio 會針對 `azuredatastudio` 存放庫，在 [GitHub 存放庫問題追蹤器](https://github.com/Microsoft/azuredatastudio/issues) \(英文\) 上追蹤問題與功能要求。 

## <a name="if-youve-experienced-any-issue"></a>如果您遇到任何問題

將問題回報給 [GitHub 問題追蹤器](https://github.com/Microsoft/azuredatastudio/issues) \(英文\)，並提供任何將有助於重現該錯誤的詳細資料。 包含來自記錄檔的所有[記錄資訊](#how-to-set-the-logging-level)。

## <a name="writing-good-bug-reports-and-feature-requests"></a>撰寫良好的錯誤 (Bug) 報表與功能要求

針對每個問題與功能要求提出單一問題。

* 不要在同一個問題中列舉多個錯誤 (Bug) 或功能要求。
* 除非您的問題來自相同的輸入，否則不要將該問題當成現有問題的註解來新增。 許多問題看起來類似，但原因不同。

您可提供的資訊越多，某人成功重現問題並找出修正方式的可能性就越大。 

在每個問題中包含下列資訊：

* Azure Data Studio 的版本
* 可重現的步驟 (1...2...3...)，以及您期望的結果與實際看到的內容。 
* 影像、動畫或影片的連結。 影像與動畫可說明重現步驟，但無法加以取代。
* 示範問題的程式碼片段或程式碼存放庫的連結，讓我們能夠輕鬆地將其提取到我們的機器上來重建問題。 

> [!NOTE]
>  由於我們需要複製並貼上程式碼片段，因此，以媒體檔案 (例如 .gif) 形式包含程式碼片段是不夠的。 

* 開發工具主控台中的錯誤 (說明 |切換開發人員工具)

請務必執行下列動作：

* 搜尋問題存放庫，以查看是否有重複的問題存在。 
* 簡化靠近問題的程式碼，以便讓問題能夠浮現出來。 

如果我們無法重現該問題並要求更多資訊，請不要有任何不好的感受！

## <a name="how-to-set-the-logging-level"></a>如何設定記錄層級

### <a name="azure-data-studio"></a>Azure Data Studio
執行 `Developer: Set Log Level...` 命令，以選取目前工作階段的記錄層級。 此值不會跨多個工作階段保存，因此如果您重新啟動 Azure Data Studio，其將還原為預設的 `Info` 層級。 

如果您想要啟用偵錯記錄以進行啟動，請將記錄層級設定為 `Debug` 並執行 `Developer: Reload Window` 命令

### <a name="mssql-built-in-extension"></a>MSSQL (內建延伸模組)

如果 `Mssql: Log Debug Info` 使用者設定已設為 True，則偵錯記錄資訊將會傳送至 `MSSQL` 輸出通道。

`Mssql: Tracing Level` 使用者設定會用來控制記錄的詳細程度。

## <a name="debug-log-location"></a>偵錯記錄位置
從 Azure Data Studio 執行 `Developer: Open Logs Folder` 命令，以開啟記錄的路徑。 有許多不同類型的記錄檔會在那裡寫入，以下為一些常用的記錄檔：

1. `renderer#.log` (例如 renderer1.log)：此檔案是主要程序的記錄檔。
1. `telemetry.log`：將記錄層級設為 `Trace` 時，此檔案將包含 Azure Data Studio 所傳送的遙測事件
1. `exthost#/exthost.log`：延伸模組主機程序的記錄檔 (這只是程序本身，而不是在其中執行的延伸模組)
1. `exthost#/Microsoft.mssql`：mssql 延伸模組的記錄，其中包含 MSSQL 相關功能的許多核心邏輯
   * sqltools.log 是 SQL 工具服務的記錄
1. `exthost#/output_logging_#######`：這些資料夾均包含 Azure Data Studio 的 `Output` 面板中所顯示的訊息。 例如，將每個檔案命名為 `#-<Channel Name>`，因此，`Notebooks` 輸出通道可能會輸出到名為 `3-Notebooks.log` 的檔案。

如果系統要求您提供記錄，請壓縮整個資料夾，以確保會包含正確的記錄。 

## <a name="next-steps"></a>後續步驟
- [回報問題](https://github.com/Microsoft/azuredatastudio/issues)
- [什麼是 Azure Data Studio](what-is-azure-data-studio.md)