---
title: 工作負載比較程式的總覽
description: 資料庫測試助理（DEA）是一個/B 測試解決方案，適用于 SQL Server 環境中的變更，例如升級或新的索引。
ms.date: 11/16/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 18cba7abf0d73197c248a62283d52126873169a3
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165756"
---
# <a name="overview-of-the-workload-comparison-process"></a>工作負載比較程式的總覽

資料庫測試助理（DEA）可協助您評估來源伺服器上的工作負載（在目前的環境中）如何在您的新環境中執行。 DEA 會藉由完成三個階段，引導您執行 A/B 測試：

- 在來源伺服器上捕獲工作負載追蹤。
- 在目標1和目標2上重新執行已捕獲的工作負載追蹤。
- 分析從目標1和目標2收集的重新執行工作負載追蹤。

這篇文章提供此程式的總覽。

## <a name="capturing-a-workload-trace"></a>捕獲工作負載追蹤

SQL Server A/B 測試的第一個階段是在來源伺服器上捕獲追蹤。 來源伺服器通常是實際執行伺服器。 追蹤檔案會在該伺服器上捕捉整個查詢工作負載，包括時間戳記。

考量因素：

- 在您開始捕獲工作負載追蹤之前，請務必先備份您要從中捕獲追蹤的資料庫。
- DEA 使用者必須設定為使用 Windows 驗證連接到資料庫。
- SQL Server 的服務帳戶需要存取來源追蹤檔案路徑。
- 若要讓 DEA 判斷查詢的效能是否已改善或降級，該查詢在捕獲期間至少必須執行15次。

## <a name="replaying-a-workload-trace"></a>重新執行工作負載追蹤

SQL Server A/B 測試的第二個階段是重新執行您在兩個目標伺服器上所捕捉的追蹤檔案：

目標1，模擬您的來源伺服器目標2，這會模擬您提議的目標環境。

[目標 1] 和 [目標 2] 的硬體設定應該盡可能類似，讓 SQL Server 可以正確地分析建議變更的效能影響。

考量因素：

- 若要重新執行工作負載追蹤，您的電腦必須設定為執行 Distributed Replay （DReplay）追蹤。
- 請務必使用來源伺服器的備份來還原目標伺服器上的資料庫。
- 建議您重新開機服務應用程式中的 SQL Server 服務（MSSQLSERVER），以改善評估結果的一致性。 SQL Server 中的查詢快取可能會影響評估結果。

## <a name="analyzing-the-replayed-workload-traces"></a>分析重新執行的工作負載追蹤

此程式的最後一個階段是使用重新執行追蹤來產生分析報表。 然後您可以查看分析報表，以取得建議變更潛在效能影響的深入解析。

考量因素：

- 如果遺失一或多個元件，當您嘗試產生新的分析報告（需要網際網路連線）時，就會出現包含下載連結的必要條件頁面。
- 若要查看使用舊版工具產生的報表，您必須先更新架構。

## <a name="see-also"></a>另請參閱

- 若要瞭解如何產生具有伺服器上所發生事件記錄檔的追蹤檔案，請參閱[Capture trace](database-experimentation-assistant-capture-trace.md)。
