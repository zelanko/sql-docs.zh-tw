---
title: 建置和發佈專案
description: 使用 SQL Server 資料庫專案延伸模組進行建置和發佈
ms.custom: seodec18
ms.date: 06/25/2020
ms.reviewer: drskwier, maghan, sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 4348f117b57c9b13a70f4a6db39ab6710eafd0ef
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/29/2020
ms.locfileid: "85519165"
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
- [資料層應用程式](../relational-databases/data-tier-applications/data-tier-applications.md)


