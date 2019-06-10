---
title: 原始檔控制
titleSuffix: Azure Data Studio
description: 了解如何在 Azure 資料 Studio 中設定原始檔控制
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 6431b869af8abc91a9de319f32c0576b82428a0a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798027"
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 中使用原始檔控制

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 支援 Git 版本/原始檔控制。


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] 中的 Git 支援

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 隨附 Git 原始檔控制管理員 (SCM)，但在使用這些功能之前，您仍然必須[安裝 Git (2.0.0 版或更新版本)](https://git-scm.com/download)。 



## <a name="open-an-existing-git-repository"></a>開啟現有的 Git 存放庫

1. 在 [檔案]  功能表下方，選取 [開啟資料夾] 
2. 瀏覽包含由 Git 追蹤之檔案的資料夾，然後按一下 [選取資料夾]  。 您可以選擇本機存放庫中的子資料夾。


## <a name="initialize-a-new-git-repository"></a>初始化新的 git 儲存機制

1. 選取 **原始檔控制**，然後選取 git 圖示。

   ![原始檔控制 git 圖示](media/source-control/source-control.png)

1. 輸入想要初始化為 Git 存放庫的資料夾路徑，然後按下 **Enter**。

   ![初始化 Git 儲存機制](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>使用 Git 存放庫

[!INCLUDE[name-sos](../includes/name-sos-short.md)] VS Code 中，會繼承其 Git 實作，但目前不支援額外的 SCM 提供者。 如需使用 Git，在您開啟或初始化存放庫後的詳細資訊，請參閱 <<c0> [ 在 VS Code 中的 Git 支援](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)。


## <a name="additional-resources"></a>其他資源
- [Git 文件](https://git-scm.com/documentation)
