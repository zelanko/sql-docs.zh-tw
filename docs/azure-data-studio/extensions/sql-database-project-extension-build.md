---
title: 建置和發佈專案
description: 使用 SQL Server 資料庫專案延伸模組進行建置和發佈
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 06/25/2020
ms.openlocfilehash: 4320873affdab74a31d1e666a84bc744b1c00385
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123172"
---
# <a name="build-and-publish-a-project"></a>建置和發佈專案

適用於 Azure Data Studio 之 SQL 資料庫專案延伸模組中的建置程序可讓您在 Windows、macOS 和 Linux 環境中建立 *dacpac*。 專案可以使用發佈程序部署到本機或雲端環境。

## <a name="prerequisites"></a>必要條件

- 安裝並設定[適用於 Azure Data Studio 的 SQL 資料庫專案延伸模組](sql-database-project-extension.md)。

## <a name="build-a-database-project"></a>建置資料庫專案

 在 [Explorer] 底下的 [專案] Viewlet 中，以滑鼠右鍵按一下 *.sqlproj* 根節點，然後選取 [建置]。

 輸出窗格將自動出現，並顯示來自建置程序的輸出。  成功的建置將會結束，並顯示下列訊息： 

 ``` ... exited with code: 0 ```

## <a name="publish-a-database-project"></a>發佈資料庫專案

透過建置程序成功編譯專案之後，就可以將資料庫發佈到 SQL Server 執行個體。 若要發佈資料庫專案，在 [Explorer] 底下的 [專案] Viewlet 中，以滑鼠右鍵按一下 *.sqlproj* 根節點，然後選取 [發佈]。

在出現的 [發行資料庫] 對話方塊中，指定伺服器連線和要建立的資料庫名稱。

## <a name="next-steps"></a>後續步驟

- [適用於 Azure Data Studio 的 SQL 資料庫專案延伸模組](sql-database-project-extension.md)
- [從命令列建置 SQL 資料庫專案](sql-database-project-extension-build-from-command-line.md)
