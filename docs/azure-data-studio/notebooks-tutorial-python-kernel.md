---
title: Azure Data Studio 中的 Python 核心筆記本
description: 本教學課程說明如何建立及執行 Python 筆記本。
author: garyericson
ms.author: garye
ms.reviewer: mikeray, alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 07/01/2020
ms.openlocfilehash: 268caea0eb9101606963dce09d33a725eb964255
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2020
ms.locfileid: "88745868"
---
# <a name="create-and-run-a-python-notebook"></a>建立及執行 Python 筆記本

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本教學課程示範如何使用 Python 核心在 Azure Data Studio 中建立及執行筆記本。

## <a name="prerequisites"></a>Prerequisites

- [已安裝 Azure Data Studio](download-azure-data-studio.md)

## <a name="create-a-notebook"></a>建立 Notebook

下列步驟說明如何在 Azure Data Studio 中建立筆記本檔案：

1. 開啟 Azure Data Studio。 如果系統提示連線到 SQL Server，則可連線或按一下 [取消]  。

1. 在 [檔案]  功能表中選取 [新增筆記本]  。

1. 針對 [核心]  選取 [Python 3]  。 [附加至] 已設定為 [localhost]。

   :::image type="content" source="media/notebook-tutorial-python/set-kernel-and-attach-to-python.png" alt-text="設定核心":::

您可從 [檔案] 功能表使用 [儲存] 或 [另存新檔...] 命令來儲存筆記本。 

若要開啟筆記本，您可從 [檔案] 功能表使用 [開啟檔案...] 命令，在 [歡迎使用] 頁面上選取 [開啟檔案]，或從命令選擇區使用 [檔案:開啟] 命令。

## <a name="change-the-python-kernel"></a>變更 Python 核心

第一次連線到筆記本中的 Python 核心時，會顯示 [為 Notebooks 設定 Python] 頁面。 您可選取下列其中一項：

- [新增 Python 安裝]  ，以安裝適用於 Azure Data Studio 的新 Python 複本，或
- [使用現有的 Python 安裝]  ，以指定現有 Python 安裝的路徑來供 Azure Data Studio 使用

若要查看使用中 Python 核心的位置和版本，請建立程式碼資料格，並執行下列 Python 命令：

```python
import os
import sys
print(sys.version_info)
print(os.path.dirname(sys.executable))
```

若要連線到不同的 Python 安裝：

1. 從 [檔案]  功能表選取 [喜好設定]  ，然後選取 [設定]  。
1. 捲動至 [延伸模組]  底下的 [筆記本組態]  。
1. 在 [使用現有的 Python]  底下，取消核取 [筆記本所使用現有 Python安裝的本機路徑] 選項。
1. 重新啟動 Azure Data Studio。

當啟動 Azure Data Studio 且連線到 Python 核心時，會顯示 [為 Notebooks 設定 Python] 頁面。您可選擇建立新的 Python 安裝，或指定現有安裝的路徑。

## <a name="run-a-code-cell"></a>執行程式碼資料格

您可建立資料格，其中包含可藉由按一下資料格左邊 [執行資料格] 按鈕 (圓形黑色箭號) 來就地執行的 SQL 程式碼。 資料格完成執行之後，會在筆記本中顯示結果。

例如：

1. 選取工具列中的 [+程式碼]  命令來新增 Python 程式碼資料格。

   :::image type="content" source="media/notebook-tutorial-python/notebook-toolbar-python.png" alt-text="筆記本工具列":::

1. 將下列範例複製並貼到資料格中，然後按一下 [執行資料格]。 此範例會執行簡單的數學運算，且結果如下所示。

   ```python
   a = 1
   b = 2
   c = a/b
   print(c)
   ```

   :::image type="content" source="media/notebook-tutorial-python/run-notebook-cell-python.png" alt-text="執行筆記本資料格":::

## <a name="next-steps"></a>後續步驟

深入了解筆記本：

- [利用 Kqlmagic 擴充 Python](notebooks-kqlmagic.md)
- [如何在 Azure Data Studio 中使用筆記本](notebooks-guidance.md)
- [建立並執行 SQL Server 筆記本](notebooks-tutorial-sql-kernel.md)
