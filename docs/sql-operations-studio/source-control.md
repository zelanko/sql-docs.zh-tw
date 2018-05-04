---
title: 原始檔控制中 SQL Operations Studio （預覽） |Microsoft 文件
description: 了解如何設定 SQL Operations Studio （預覽） 中的原始檔控制。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 58475a1c7bfb27f29c1e040de286c82d9c7a204f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>使用原始檔控制中 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 版本/原始檔控制中支援 Git。


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>中的 Git 支援 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 隨附 Git 原始檔控制管理員 (SCM)，但是您仍然需要[安裝 Git (2.0.0 版或更新版本)](https://git-scm.com/download)之前可提供下列功能。 



## <a name="open-an-existing-git-repository"></a>開啟現有的 Git 儲存機制

1. 在下**檔案**功能表上，選取**開啟資料夾...**
2. 瀏覽至包含由 git，追蹤檔案的資料夾，然後按一下 **選取資料夾**。 在本機儲存機制中的子資料夾是可以在這裡選取的。


## <a name="initialize-a-new-git-repository"></a>初始化新的 git 儲存機制

1. 選取**原始檔控制**，然後選取 git 圖示。

   ![原始檔控制 git 圖示](media/source-control/source-control.png)

1. 輸入您想要初始化為 Git 儲存機制和按下的資料夾路徑**Enter**。

   ![初始化 Git 儲存機制](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>使用 Git 儲存機制

[!INCLUDE[name-sos](../includes/name-sos-short.md)] VS Code 會繼承其 Git 實作，但目前不支援其他 SCM 提供者。 如需使用 Git 之後您開啟或初始化儲存機制, 的詳細資訊，請參閱[VS 程式碼中的 Git 支援](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)。


## <a name="additional-resources"></a>其他資源
- [Git 文件](https://git-scm.com/documentation)
