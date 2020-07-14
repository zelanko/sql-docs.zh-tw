---
title: 使用機器學習延伸模組來管理套件
titleSuffix: Azure Data Studio
description: 了解如何使用適用於 Azure Data Studio 的機器學習延伸模組，來管理資料庫中的 Python 或 R 套件。
ms.date: 05/19/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 234c7493852afb4667f9c97b2cb4bb81e119af63
ms.sourcegitcommit: 48d60fe6b6991303a88936fb32322c005dfca2d8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2020
ms.locfileid: "85352395"
---
# <a name="manage-packages-in-database-with-machine-learning-extension-preview-for-azure-data-studio"></a>使用適用於 Azure Data Studio 的機器學習延伸模組 (預覽) 來管理資料庫中的套件

了解如何使用[適用於 Azure Data Studio 的機器學習延伸模組](machine-learning-extension.md)，來管理資料庫中的 Python 或 R 套件。

> [!IMPORTANT]
> 使用機器學習延伸模組來管理資料庫中的套件，目前僅支援 SQL Server 2019 上的[機器學習服務](../machine-learning/sql-server-machine-learning-services.md)。

## <a name="prerequisites"></a>必要條件

- 安裝並設定[適用於 Azure Data Studio 的機器學習延伸模組](machine-learning-extension.md)。 您必須[在 [延伸模組設定] 中指定 Python 或 R 安裝路徑](machine-learning-extension.md#settings)，套件管理才能正常運作。

- **sqlmlutils** 套件。 如果套件尚未安裝，機器學習延伸模組將提示您安裝此套件。

- 針對 Linux 上的 SQL Server，不支援使用 Windows 驗證。 因此，您必須使用 SQL 驗證來連線到 Linux 上的 SQL Server。

## <a name="manage-python-packages"></a>管理 Python 套件

您可以使用機器學習延伸模組來安裝和解除安裝 Python 套件。

### <a name="install-new-python-package"></a>安裝新的 Python 套件

遵循下列步驟，在您的資料庫中安裝 Python 套件。

1. 按一下 [管理資料庫中的套件]。

1. 如果系統要求您安裝 **sqlmlutils**，按一下 [是]。

1. 在 [已安裝] 索引標籤底下，選取 [套件類型] 底下的 [Python]，然後選取 [位置] 底下的資料庫。

1. 按一下 [新增] 索引標籤。

1. 在 [搜尋 Python 套件] 中，輸入您想要安裝的 Python 套件，然後按一下 [搜尋]。

1. 確認套件已列於 [套件名稱] 底下，而且所需版本已列於 [套件版本] 底下。

1. 按一下 [Install] 。

1. 按一下 [關閉]，並在 [工作] 底下確認套件已成功安裝。

### <a name="uninstall-a-python-package"></a>解除安裝 Python 套件

遵循下列步驟，在您的資料庫中解除安裝 Python 套件。

> [!NOTE]
> 您只能解除安裝已安裝於資料庫中的套件。 您無法將已隨同 SQL Server 機器學習服務預先安裝的套件解除安裝。

1. 按一下 [管理資料庫中的套件]。

1. 如果系統要求您安裝 **sqlmlutils**，按一下 [是]。

1. 在 [已安裝] 索引標籤底下，選取 [套件類型] 底下的 [Python]，然後選取 [位置] 底下的資料庫。

1. 選取您要解除安裝的套件。

1. 按一下 [將選取的套件解除安裝]。

1. 按一下 [關閉]，並在 [工作] 底下確認套件已成功安裝。

## <a name="manage-r-packages"></a>管理 R 套件

您可以使用機器學習延伸模組來安裝和解除安裝 R 套件。

### <a name="install-new-r-package"></a>安裝新的 R 套件

遵循下列步驟，在您的資料庫中安裝 Python 套件。

1. 按一下 [管理資料庫中的套件]。

1. 如果系統要求安裝 **sqlmlutils**，按一下 [是]。

1. 在 [已安裝] 索引標籤底下，選取 [套件類型] 底下的 [R]，然後選取 [位置] 底下的資料庫。

1. 按一下 [新增] 索引標籤。

1. 在 [搜尋 R 套件] 中，輸入您想要安裝的 R 套件，然後按一下 [搜尋]。

1. 確認套件已列於 [套件名稱] 底下，而且所需版本已列於 [套件版本] 底下。

1. 按一下 [Install] 。

1. 按一下 [關閉]，並在 [工作] 底下確認套件已成功安裝。

### <a name="uninstall-an-r-package"></a>解除安裝 R 套件

遵循下列步驟，在您的資料庫中解除安裝 R 套件。

> [!NOTE]
> 您只能解除安裝已安裝於資料庫中的套件。 您無法將已隨同 SQL Server 機器學習服務預先安裝的套件解除安裝。

1. 按一下 [管理資料庫中的套件]。

1. 如果系統要求安裝 **sqlmlutils**，按一下 [是]。

1. 在 [已安裝] 索引標籤底下，選取 [套件類型] 底下的 [R]，然後選取 [位置] 底下的資料庫。

1. 選取您要解除安裝的套件。

1. 按一下 [將選取的套件解除安裝]。

1. 按一下 [關閉]，並在 [工作] 底下確認套件已成功安裝。

## <a name="next-steps"></a>後續步驟

- [Azure Data Studio 中的機器學習延伸模組](machine-learning-extension.md)
- [進行預測](machine-learning-extension-predictions.md)
- [匯入或檢視模型](machine-learning-extension-import-view-models.md)
- [Azure Data Studio 中的 Notebook](notebooks-guidance.md)
- [SQL 機器學習文件](../machine-learning/index.yml)
