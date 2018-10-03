---
title: 原始檔控制中 Azure Data Studio |Microsoft Docs
description: 了解如何在 Azure 資料 Studio 中設定原始檔控制。
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2dd424922c4f21c8822a74c49b56723467ac6fed
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "48038075"
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>使用中的原始檔控制 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 支援 Git 版本/原始檔控制。


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>中的 Git 支援 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 隨附於 Git 原始檔控制管理員 (SCM)，但您仍然要[安裝 Git (2.0.0 版或更新版本)](https://git-scm.com/download)均提供這些功能之前。 



## <a name="open-an-existing-git-repository"></a>開啟現有的 Git 存放庫

1. 底下**檔案**功能表上，選取**開啟資料夾...**
2. 瀏覽至 git，來追蹤您檔案所在的資料夾，然後按一下**選取資料夾**。 在本機儲存機制中的子資料夾是可以在此處選取的。


## <a name="initialize-a-new-git-repository"></a>初始化新的 git 儲存機制

1. 選取 **原始檔控制**，然後選取 git 圖示。

   ![原始檔控制 git 圖示](media/source-control/source-control.png)

1. 輸入您想要初始化為 Git 儲存機制和按下的資料夾路徑**Enter**。

   ![初始化 Git 儲存機制](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>使用 Git 存放庫

[!INCLUDE[name-sos](../includes/name-sos-short.md)] VS Code 中，會繼承其 Git 實作，但目前不支援額外的 SCM 提供者。 如需使用 Git，在您開啟或初始化存放庫後的詳細資訊，請參閱 <<c0> [ 在 VS Code 中的 Git 支援](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)。


## <a name="additional-resources"></a>其他資源
- [Git 文件](https://git-scm.com/documentation)
