---
title: SQL Server dacpac 延伸模組
titleSuffix: Azure Data Studio
description: 安裝和使用適用於 Azure 資料 Studio 的 SQL Server dacpac 延伸模組 （預覽）
ms.custom: seodec18
ms.date: 03/18/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: e40e377310b33034b4abecdc5e58eab17d39695d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959190"
---
# <a name="sql-server-dacpac-extension-preview"></a>SQL Server dacpac 延伸模組 (預覽)

**資料層應用程式精靈**提供簡單易用的經驗，部署和擷取.dacpac 檔案以及匯入和匯出.bacpac 檔案。

這項體驗目前處於其初始的預覽階段。 請回報問題和功能要求[這裡。](https://github.com/microsoft/azuredatastudio/issues)

![資料動作](media/sql-server-dacpac-extension/data-tier-application-actions.png)

 ### <a name="requirements"></a>需求
 * 此精靈需要啟動 SQL Server 執行個體的作用中連接。

 ### <a name="how-do-i-start-the-data-tier-application-wizard"></a>如何啟動 [資料層應用程式精靈]？
 * 精靈的主要進入點是以滑鼠右鍵按一下 [物件總管] 中的資料庫，然後按一下**資料層應用程式精靈**。
 * 如果使用者連接到 SQL Server 執行個體，使用者也可以啟動精靈從命令選擇區 (Ctrl + Shift + P) 藉由搜尋**資料層應用程式精靈。**

 ### <a name="why-would-i-use-the-data-tier-application-wizard"></a>為什麼我要使用的資料層應用程式精靈？
 若要新增的功能擷取及部署.dacpac 檔案匯入和匯出.bacpac 檔案，在 Azure 資料 Studio 中的建立此精靈。

## <a name="install-the-sql-server-dacpac-extension"></a>安裝 SQL Server dacpac 擴充功能

1. 若要開啟擴充管理員及存取可用的擴充功能，選取 [擴充功能] 圖示，或選取**檢視**功能表中的**擴充功能**。
2. 選取 SQL Server dacpac 延伸模組，然後按一下**安裝**。
1. 選取**重新載入**以啟用該擴充功能 (只有第一次安裝擴充功能時需要)。
2. 透過滑鼠右鍵點選伺服器或資料庫並點選**管理**，瀏覽您的管理儀表板。
3. 已安裝的擴充功能會以索引標籤方式顯示在您的管理儀表板上：

## <a name="next-steps"></a>後續步驟

若要深入了解 dacpac，[檢查我們的文件。](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)