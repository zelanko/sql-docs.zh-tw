---
title: SQL Server Agent 延伸模組
description: 了解如何安裝和使用適用於 Azure Data Studio 的 SQL Server Agent 延伸模組，這是一種用於管理 SQL Agent 作業和設定的延伸模組。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 3d00919c0967db12dfe678ad541a5a9ed9ecae61
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123121"
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

   ![安裝代理程式](media/sql-server-agent-extension/install-sql-agent.png)

3. 選取您想要的延伸模組並加以**安裝**。
4. 選取 [重新載入]，啟用此延伸模組 (只有當您第一次安裝延伸模組時才需要)。
5. 以滑鼠右鍵按一下您的伺服器或資料庫，然後選取 [管理]，巡覽至您的管理儀表板。
6. 已安裝的延伸模組會顯示為管理儀表板上的索引標籤：

   ![檢視代理程式](media/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>檢視作業

當您連線到 SQL Server Agent 延伸模組時，首先會看到您所有的 Agent 作業清單。

   ![檢視作業](media/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server Agent，請[參閱我們的文件](../../ssms/agent/sql-server-agent.md)。
