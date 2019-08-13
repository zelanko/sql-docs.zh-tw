---
title: SQL Server dacpac 延伸模組
titleSuffix: Azure Data Studio
description: 安裝和使用適用於 Azure Data Studio 的 SQL Server dacpac 延伸模組 (預覽)
ms.custom: seodec18
ms.date: 03/18/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: e40e377310b33034b4abecdc5e58eab17d39695d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959190"
---
# <a name="sql-server-dacpac-extension-preview"></a>SQL Server dacpac 延伸模組 (預覽)

「資料層應用程式精靈」  提供便於部署和解壓縮 .dacpac 檔案，以及匯入和匯出 .bacpac 檔案的使用體驗。

此體驗目前為初始預覽狀態。 請在[這裡](https://github.com/microsoft/azuredatastudio/issues)回報問題和功能要求。

![資料動作](media/sql-server-dacpac-extension/data-tier-application-actions.png)

 ### <a name="requirements"></a>需求
 * 此精靈需要與 SQL Server 執行個體進行使用中連線才能啟動。

 ### <a name="how-do-i-start-the-data-tier-application-wizard"></a>如何啟動「資料層應用程式精靈」？
 * 此精靈的主要進入點是以滑鼠右鍵按一下物件總管中的資料庫，然後按一下 [Data-tier Application wizard] \(資料層應用程式精靈\)  。
 * 如果使用者已連線到 SQL Server 執行個體，使用者也可以從命令選擇區 (Ctrl + Shift + P) 搜尋「資料層應用程式精靈」  啟動精靈。

 ### <a name="why-would-i-use-the-data-tier-application-wizard"></a>為什麼使用「資料層應用程式精靈」？
 此精靈建立的目的是為了在 Azure Data Studio 中新增解壓縮和部署 .dacpac 檔案，以及匯入和匯出 .bacpac 檔案的功能。

## <a name="install-the-sql-server-dacpac-extension"></a>安裝 SQL Server dacpac 延伸模組

1. 若要開啟延伸模組管理員並存取可用的延伸模組，請選取延伸模組圖示，或選取 [檢視]  功能表中的 [延伸模組]  。
2. 選取 SQL Server dacpac 延伸模組，然後按一下 [安裝]  。
1. 選取 [重新載入]  ，啟用此延伸模組 (只有當您第一次安裝延伸模組時才需要)。
2. 以滑鼠右鍵按一下您的伺服器或資料庫，然後選取 [管理]  ，巡覽至您的管理儀表板。
3. 已安裝的延伸模組會顯示為管理儀表板上的索引標籤：

## <a name="next-steps"></a>後續步驟

若要深入了解 dacpac，請[參閱我們的文件](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)。