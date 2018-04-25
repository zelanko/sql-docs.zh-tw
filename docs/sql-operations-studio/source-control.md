---
title: "SQL Operations Studio（預覽）的原始碼控制  |Microsoft 文件"
description: "學習如何設定 SQL Operations Studio （預覽）的原始碼控制。"
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f28199262b087ad5362da0ddf56827216aec748
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 使用原始碼控制

[!INCLUDE[name-sos](../includes/name-sos-short.md)]支援 Git 版本/原始碼控制。


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 的 Git 支援

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 內附 Git 原始碼控制管理員 (SCM)，但是在使用功能之前，您仍然需要[安裝 Git (2.0.0 版或更新版本)](https://git-scm.com/download)。 



## <a name="open-an-existing-git-repository"></a>開啟現有的 Git 儲存庫

1. 在**檔案**功能表下，選取**開啟資料夾...**
2. 瀏覽至包含 git 追蹤檔案的資料夾，然後按一下 **選取資料夾**。在這裡可以選取本機儲存庫的子資料夾。


## <a name="initialize-a-new-git-repository"></a>初始化新的 git 儲存機制

1. 選取**原始檔控制**，然後選取 git 圖示。

   ![原始檔控制 git 圖示](media/source-control/source-control.png)

1. 輸入您想要初始化為 Git 儲存庫的資料夾路徑然後按下**Enter**。

   ![初始化 Git 儲存機制](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>使用 Git 儲存庫

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 會從 VS Code 繼承其 Git 實作，但目前不支援其他 SCM 提供者。在您開啟或初始化儲存庫之後，如需使用 Git 的詳細資訊，請參閱 [VS Code 中的 Git 支援](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support)。


## <a name="additional-resources"></a>其他資源
- [Git 文件](https://git-scm.com/documentation)
