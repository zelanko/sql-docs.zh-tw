---
title: Azure Arc 延伸模組 (預覽)
description: 了解如何安裝和使用 Azure Arc 延伸模組來試用 Azure Arc 資料服務。
ms.custom: seodec18
ms.date: 09/22/2020
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 53adb48f8ee83213fe99eee1148173d20c6276c7
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942374"
---
# <a name="azure-arc-extension-for-azure-data-studio-preview"></a>適用於 Azure Data Studio 的 Azure Arc 延伸模組 (預覽)

[Azure Arc 延伸模組 (預覽)](https://aka.ms/azurearcdata-docs) 是用於建立和管理 Azure Arc 資料服務資源的延伸模組。

**主要動作包括：**
- 建立資源
    - 資料控制器
    - 適用於 Azure Arc 的 SQL 受控執行個體
    - 適用於 Azure Arc 的 PostgreSQL
- 管理資源
    - 檢視資料控制器儀表板
    - 檢視適用於 Azure Arc 的 SQL 受控執行個體儀表板
    - 檢視適用於 Azure Arc 的 PostgreSQL 儀表板
- 執行 Azure Arc Jupyter Book

## <a name="install-the-extension"></a>安裝延伸模組
- 從資源庫安裝 [Azure Data CLI] 延伸模組。
- 從資源庫安裝 [Azure Arc] 延伸模組。
- 重新啟動 Azure Data Studio

## <a name="sign-in-with-azure-account"></a>使用 Azure 帳戶登入
1. 選取左下方的 [帳戶]
1. 選取 [新增帳戶]
1. 此動作會啟動瀏覽器。 登入您的 Azure 帳戶。

## <a name="create-a-resource"></a>建立資源
此延伸模組支援 Azure Arc 資料控制器的部署、適用於 Azure Arc 的 Postgres，以及適用於 Azure Arc 的 SQL 受控執行個體。您可透過內建的部署精靈來完成部署。

1. 在左側活動列上選取 [連線] Viewlet
1. 選取三個點，然後選取 [新增部署]
1. 遵循提示以建立新的 Azure Arc 資源。

## <a name="manage-a-resource"></a>管理資源
從 azdata、Azure 入口網站或 Azure Data Studio 部署 Azure Arc 資料控制器之後，您可以從 Azure Data Studio 連線到該控制器。

1. 在左側活動列上開啟 [連線] Viewlet。
1. 展開 [Azure Arc 控制器]
1. 選取 [連線控制器]
1. 填妥參數並連線。

連線之後，您就可以查看資料控制器上部署的資源。 然後，您可以按一下滑鼠右鍵並選取 [管理]，以存取資源儀表板。  

這些儀表板會提供資源的其他相關資訊，包括在 Azure 入口網站中開啟的選項。

## <a name="next-steps"></a>下一步
若要深入了解 Azure Arc 資料服務，請[查看我們的文件。](https://aka.ms/azurearcdata-docs)
