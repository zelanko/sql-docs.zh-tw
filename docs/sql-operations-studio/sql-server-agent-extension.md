---
title: SQL Operations Studio （預覽） SQL Server Agent 擴充功能 |Microsoft Docs
description: SQL Operations Studio （預覽） 的 SQL Server Agent 擴充功能
ms.custom: tools|sos
ms.date: 07/19/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 0da107a9f5dab0a9eb468bc3570788cff816b24a
ms.sourcegitcommit: 4b21840f20195d70f255465666f7b409ba839d18
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2018
ms.locfileid: "39147012"
---
# <a name="sql-server-agent-extension"></a>SQL Server Agent 擴充功能

SQL Server Agent 擴充功能是管理和疑難排解 SQL Agent 作業和組態的擴充功能。 此延伸模組目前為預覽狀態。

主要工作包括：
- 列出在 SQL Server 上設定的 SQL Server Agent 作業
- 檢視作業歷程記錄與工作執行結果
- 啟動和停止作業的基本作業控制

## <a name="install-the-sql-server-agent-extension"></a>安裝 SQL Server Agent 擴充功能

1. 若要開啟擴充管理員及存取可用的擴充功能，選取 [擴充功能] 圖示，或選取**檢視**功能表中的**擴充功能**。
2. 選取可用的擴充功能以檢視其詳細資料。

   ![安裝代理程式](media/extensions/sql-server-agent-extension/install-sql-agent.png)

1. 選取您想要的延伸模組並**安裝**它。
2. 選取**重新載入**以啟用該擴充功能 (只有第一次安裝擴充功能時需要)。
1. 透過滑鼠右鍵點選伺服器或資料庫並點選**管理**，瀏覽您的管理儀表板。

2. 已安裝的擴充功能會以索引標籤方式顯示在您的管理儀表板上：

   ![檢視代理程式](media/extensions/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>檢視作業

當您連接到 SQL Server Agent 延伸模組時，您會看到第一個東西是一份您所有的 Agent 作業清單。

   ![檢視作業](media/extensions/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server Agent，[檢查我們的文件。](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent?view=sql-server-2017)


