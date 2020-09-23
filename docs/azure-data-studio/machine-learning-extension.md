---
title: 機器學習延伸模組 (預覽)
titleSuffix: Azure Data Studio
description: 適用於 Azure Data Studio 的機器學習延伸模組可讓您管理套件、匯入機器學習模型、進行預測，以及建立筆記本來執行 SQL 資料庫的實驗。
ms.date: 05/19/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: a6a86baeb3c206c722aa91eae386ca80c287644c
ms.sourcegitcommit: b9871e6cffb4c2c65d1f27f797630c43fc02cfb0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101118"
---
# <a name="machine-learning-extension-preview-for-azure-data-studio"></a>適用於 Azure Data Studio 的機器學習延伸模組 (預覽)

適用於 [Azure Data Studio](what-is.md) 的機器學習延伸模組可讓您管理套件、匯入機器學習模型、進行預測，以及建立筆記本來執行 SQL 資料庫的實驗。 此延伸模組目前為預覽狀態。

## <a name="prerequisites"></a>必要條件

您必須在執行 Azure Data Studio 的電腦上安裝下列先決條件。

- [Python 3](https://www.python.org/downloads/)。 安裝 Python 之後，您必須在 [[延伸模組設定](#settings)] 底下，指定 Python 安裝的本機路徑。 如果您已在 Azure Data Studio 中使用 [Python 核心筆記本](notebooks-tutorial-python-kernel.md)，根據預設，此延伸模組將使用來自筆記本的路徑。

- 適用於 Windows、macOS 或 Linux 的 [Microsoft ODBC Driver 17 for SQL Server](../connect/odbc/download-odbc-driver-for-sql-server.md)。

- [R 3.5](https://www.r-project.org/) (選擇性)。 目前不支援 3.5 以外的其他版本。 安裝 R 3.5 之後，您必須啟用 R，並在 [[延伸模組設定](#settings)] 底下，指定 R 安裝的本機路徑。 只有當您想要管理資料庫中的 R 套件時，才需要執行此動作。

### <a name="trouble-installing-python-3-from-within-ads"></a>無法從 ADS 內安裝 Python 3 嗎？
如果您嘗試安裝 Python 3，但收到關於 TLS/SSL 的錯誤，請新增這兩個選擇性元件：

_範例錯誤：_
```
$: ~/0.0.1/bin/python3 -m pip install --user "jupyter>=1.0.0" --extra-index-url https://prose-python-packages.azurewebsites.net
WARNING: pip is configured with locations that require TLS/SSL, however the ssl module in Python is not available.
Looking in indexes: https://pypi.org/simple, https://prose-python-packages.azurewebsites.net
Requirement already satisfied: jupyter
```

_安裝這些元件：_

- [Homebrew](https://brew.sh) (選擇性)。 安裝 homebrew，然後從命令列執行 `brew update`。

- *openssl* (選擇性)。 接著，執行 `brew install openssl`。

## <a name="install-the-extension"></a>安裝延伸模組

若要在 Azure Data Studio 中安裝機器學習延伸模組，請遵循下列步驟。

1. 在 Azure Data Studio 中開啟延伸模組管理員。 您可以選取延伸模組圖示，或在 [檢視] 功能表中選取 [延伸模組]。

1. 選取 [機器學習] 延伸模組，並檢視其詳細資料。

1. 按一下 [Install] 。

1. 按一下 [重新載入] 以啟用延伸模組。 只有在您第一次安裝延伸模組時，才需執行此動作。

<a name="settings"></a>

## <a name="extension-settings"></a>延伸模組設定

若要變更機器學習延伸模組的設定，請遵循下列步驟。

1. 在 Azure Data Studio 中開啟延伸模組管理員。 您可以選取延伸模組圖示，或在 [檢視] 功能表中選取 [延伸模組]。

1. 在 [已啟用] 延伸模組底下，尋找**機器學習**延伸模組。

1. 按一下 [管理] 圖示。

1. 按一下 [延伸模組設定] 圖示。

延伸模組設定看起來像這樣：

:::image type="content" source="media/machine-learning-extension/ml-extension-settings.png" alt-text="機器學習延伸模組設定":::

### <a name="enable-python"></a>啟用 Python

若要在資料庫中使用機器學習延伸模組以及 Python 套件管理，請遵循下列步驟。

> [!IMPORTANT]
> 即使您不想在資料庫功能中使用 Python 套件管理，機器學習延伸模組還是必須啟用 Python，並設定為大部分功能均可運作。

1. 確定 [機器學習:啟用 Python] 已啟用。 此設定預設為啟用狀態。

1. 提供您預先存在之 Python 安裝的路徑 (位於 [機器學習:Python 路徑] 底下)。 這可以是 Python 可執行檔的完整路徑，也可以是可執行檔所在的資料夾。 如果您已在 Azure Data Studio 中使用 [Python 核心筆記本](notebooks-tutorial-python-kernel.md)，根據預設，此延伸模組將使用來自筆記本的路徑。

### <a name="enable-r"></a>啟用 R

若要在資料庫中使用適用於 R 套件管理的機器學習延伸模組，請遵循下列步驟。

1. 確定 [機器學習:啟用 R] 已啟用。 預設會停用此設定。

1. 提供您預先存在之 R 安裝的路徑 (位於 [機器學習:R 路徑] 底下)。 這必須是 R 可執行檔的完整路徑。 

## <a name="use-the-machine-learning-extension"></a>使用機器學習延伸模組

若要在 Azure Data Studio 中使用機器學習延伸模組，請遵循下列步驟。

1. 在 Azure Data Studio 中開啟 [連線] Viewlet。

1. 在您的伺服器上按一下滑鼠右鍵，然後選取 [管理]。

1. 在左側功能表中的 [一般] 底下，按一下 [機器學習]。

遵循**後續步驟**底下的連結，以查看如何使用機器學習延伸模組來管理套件、進行預測，以及在資料庫中匯入模型。

## <a name="next-steps"></a>後續步驟

- [管理資料庫中的套件](machine-learning-extension-manage-packages.md)
- [進行預測](machine-learning-extension-predictions.md)
- [匯入或檢視模型](machine-learning-extension-import-view-models.md)
- [Azure Data Studio 中的 Notebook](notebooks-guidance.md)
- [SQL 機器學習文件](../machine-learning/index.yml)
- [SQL Edge (預覽) 中採用 ONNX 的機器學習和 AI](/azure/azure-sql-edge/onnx-overview)
