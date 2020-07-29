---
title: SQL Server Distributed Replay
titleSuffix: SQL Server Distributed Replay
description: SQL Server Distributed Replay 功能可協助您評估未來 SQL Server、硬體與作業系統的升級，以及 SQL Server 調整的影響。
ms.prod: sql
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 58ef7016-b105-42c2-90a0-364f411849a4
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 2083c38c426b9a684badf664dfbdad5de53b7c14
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85732187"
---
# <a name="sql-server-distributed-replay"></a>SQL Server Distributed Replay

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 功能可協助您評定未來 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級的影響。 您也可以使用它來協助評估硬體和作業系統升級以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 微調的影響。

## <a name="benefits-of-distributed-replay"></a>Distributed Replay 的優點

與 SQL Server Profiler 相似之處在於，您可使用 Distributed Replay，針對已升級的測試環境重新執行擷取的追蹤。 而與 SQL Server Profiler 不同的是，Distributed Replay 不限於從單一電腦重新執行工作負載。

Distributed Replay 提供比 SQL Server Profiler 更容易調整的解決方案。 您可以使用 Distributed Replay，從多部電腦重新執行工作負載，並有效地模擬關鍵任務的工作負載。

[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 功能可以使用多部電腦來重新執行追蹤資料，並模擬任務關鍵性工作負載。 您可以使用 Distributed Replay 進行應用程式相容性測試、效能測試或容量計畫。

## <a name="when-to-use-distributed-replay"></a>使用 Distributed Replay 的時機

SQL Server Profiler 和 Distributed Replay 所提供的功能有部分重疊。

您可使用 SQL Server Profiler 針對升級的測試環境重新執行所擷取追蹤。 您也可以分析重新執行結果，以便尋找可能的功能與效能不相容。 不過，SQL Server Profiler 只能從單一電腦重新執行工作負載。 重新執行具有許多使用中並行連線或高輸送量的密集型 OLTP 應用程式時，SQL Server Profiler 可能會變成資源瓶頸。

Distributed Replay 提供比 SQL Server Profiler 更容易調整的解決方案。 您可以使用 Distributed Replay，從多部電腦重新執行工作負載，並有效地模擬關鍵任務工作負載。

下表將描述使用每項工具的時機。

|工具|使用時機...|
|----------|---------------|
| SQL Server Profiler | 您想要在單一電腦上使用傳統的重新執行機制。 尤其，您需要逐行偵錯功能，例如 [步驟]、[執行至資料指標處] 及 [切換中斷點] 命令。<br /><br /> 您想要重新執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 追蹤。 |
| Distributed Replay |您想要評估應用程式相容性。 例如，您想要測試 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和作業系統升級狀況、硬體升級或索引微調。<br /><br /> 擷取追蹤中的並行過高，導致單一重新執行用戶端無法充分進行模擬。|  

## <a name="distributed-replay-concepts"></a>Distributed Replay 概念

下列元件構成 Distributed Replay 環境：  

- **Distributed Replay 系統管理工具**：用來與 Distributed Replay Controller 進行通訊的主控台應用程式 **DReplay.exe**。 您可以使用管理工具來控制分散式重新執行。  

- **Distributed Replay Controller**：執行 Windows 服務且名為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller 的電腦。 Distributed Replay Controller 可協調 Distributed Replay Client 的動作。 每個 Distributed Replay 環境都只能有一個 Controller 執行個體。  

- **Distributed Replay Client**：一或多部執行 Windows 服務且名為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 的 (實體或虛擬) 電腦。 Distributed Replay Client 會共同運作以模擬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的工作負載。 每個 Distributed Replay 環境中可以有一個或多個用戶端。  

- **目標伺服器**：Distributed Replay Client 可用來重新執行追蹤資料的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 我們建議將目標伺服器放置於測試環境中。

Distributed Replay 管理工具、Controller 及 Client 可以安裝在不同的電腦上，也可以安裝在同一部電腦上。 在同一部電腦上，只能執行一個 Distributed Replay Controller 或 Client 服務的執行個體。

下圖顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 實體架構：  

![Distributed Replay 架構](../../tools/distributed-replay/media/distributedreplayarch.gif "Distributed Replay 架構")  

## <a name="distributed-replay-tasks"></a>Distributed Replay 工作

|工作描述|主題|  
|----------------------|-----------|  
| 描述如何設定 Distributed Replay。 | [設定 Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md) |
| 描述如何準備輸入追蹤資料。 | [準備輸入追蹤資料](../../tools/distributed-replay/prepare-the-input-trace-data.md) |
| 描述如何重新執行追蹤資料。 |[重新執行追蹤資料](../../tools/distributed-replay/replay-trace-data.md) | | 描述如何檢閱 Distributed Replay 追蹤資料結果。 |[檢閱重新執行的結果](../../tools/distributed-replay/review-the-replay-results.md)|
| 描述如何使用管理工具來起始、監視和取消控制器上的作業。 | [管理工具命令列選項 &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md) |

## <a name="see-also"></a>另請參閱

[SQL Server Distributed Replay 論壇](https://social.technet.microsoft.com/Forums/sl/sqldru/)