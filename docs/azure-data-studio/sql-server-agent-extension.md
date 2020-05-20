---
title: SQL Server Agent 延伸模組
titleSuffix: Azure Data Studio
description: 安裝和使用適用於 Azure Data Studio 的 SQL Server Agent 延伸模組 (預覽)
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 05356cc815fdba22d55ee339d60994f2c9423373
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "67959182"
---
# <a name="sql-server-agent-extension-preview"></a>SQL Server Agent 延伸模組 (預覽)

SQL Server Agent 延伸模組 (預覽) 是用於管理 SQL Agent 作業和設定，並進行疑難排解的延伸模組。 此延伸模組目前為預覽狀態。

主要動作包括：
- 列出在 SQL Server 上設定的 SQL Server Agent 作業
- 檢視包含作業執行結果的作業記錄
- 啟動和停止作業的基本作業控制

## <a name="install-the-sql-server-agent-extension"></a>安裝 SQL Server Agent 延伸模組

1. 若要開啟延伸模組管理員並存取可用的延伸模組，請選取延伸模組圖示，或選取 [檢視] 功能表中的 [延伸模組]。
2. 選取可用的延伸模組，檢視詳細資料。

   ![安裝代理程式](media/extensions/sql-server-agent-extension/install-sql-agent.png)

1. 選取您想要的延伸模組並加以**安裝**。
2. 選取 [重新載入]  ，啟用此延伸模組 (只有當您第一次安裝延伸模組時才需要)。
1. 以滑鼠右鍵按一下您的伺服器或資料庫，然後選取 [管理]  ，巡覽至您的管理儀表板。
2. 已安裝的延伸模組會顯示為管理儀表板上的索引標籤：

   ![檢視代理程式](media/extensions/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>檢視作業

當您連線到 SQL Server Agent 延伸模組時，首先會看到您所有的 Agent 作業清單。

   ![檢視作業](media/extensions/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server Agent，請[參閱我們的文件](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent?view=sql-server-2017)。


