---
title: Azure Data Studio 中的 Python 核心筆記本
description: 本教學課程說明如何建立及執行 Python 筆記本。
author: garyericson
ms.author: garye
ms.reviewer: mikeray, alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: ''
ms.custom: ''
ms.date: 04/27/2020
ms.openlocfilehash: e4c431cba395b8e0c732fa7ac4ab96942cac7144
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728858"
---
# <a name="create-and-run-a-python-notebook"></a>建立及執行 Python 筆記本

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本教學課程示範如何使用 Python 核心在 Azure Data Studio 中建立及執行筆記本。

## <a name="prerequisites"></a>Prerequisites

- [已安裝 Azure Data Studio](download-azure-data-studio.md)

## <a name="new-notebook"></a>新增筆記本

下列步驟說明如何在 Azure Data Studio 中建立筆記本檔案：

1. 開啟 Azure Data Studio。 如果系統提示連線到 SQL Server，則可連線或按一下 [取消]  。

1. 在 [檔案]  功能表中選取 [新增筆記本]  。

1. 針對 [核心]  選取 [Python 3]  。

   :::image type="content" source="media/notebook-tutorial-python/set-kernel-and-attach-to-python.png" alt-text="設定核心":::

1. 如果系統提示設定 Python，則請在 [為筆記本設定 Python]  中選取下列其中一項：

   - [新增 Python 安裝]  ，以安裝適用於 Azure Data Studio 的新 Python 複本，或
   - [使用現有的 Python 安裝]  ，以指定現有 Python 安裝的路徑

## <a name="run-a-notebook-cell"></a>執行筆記本資料格

您可建立包含程式碼或文字的資料格。 您可就地執行程式碼資料格，在資料格完成執行之後，結果將顯示在筆記本中。 文字資料格可供使用程式碼來穿插格式化的文件。

### <a name="code"></a>程式碼

選取工具列中的 [+程式碼]  命令來新增 Python 程式碼資料格。

:::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python.png" alt-text="筆記本工具列":::

此範例會執行簡單的數學運算。

```python
a = 1
b = 2
c = a/b
print(c)
```
按一下資料格左側的播放按鈕來執行資料格。 結果如下所示。

:::image type="content" source="media/notebook-tutorial-python/run-notebook-cell-python.png" alt-text="執行筆記本資料格":::

### <a name="text"></a>Text

選取工具列中的 [+文字]  命令來新增新文字儲存格。

:::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python-text.png" alt-text="筆記本工具列":::

資料格會變更為編輯模式；現在當鍵入 Markdown 時，即可同時查看預覽。

:::image type="content" source="media/notebook-tutorial-python/notebook-markdown-cell-python.png" alt-text="Markdown 資料格":::

選取文字資料格以外的地方只會顯示 Markdown 文字。

:::image type="content" source="media/notebook-tutorial-python/notebook-markdown-preview-python.png" alt-text="Markdown 文字":::

## <a name="next-steps"></a>後續步驟

深入了解筆記本：

- [如何搭配 SQL Server 使用筆記本](notebooks-guidance.md)

- [建立並執行 SQL Server 筆記本](notebooks-tutorial-sql-kernel.md)

- [如何管理 Azure Data Studio 中的 Notebook](notebooks-manage-sql-server.md)
