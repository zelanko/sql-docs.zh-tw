---
title: 使用機器學習延伸模組匯入或檢視模型
titleSuffix: Azure Data Studio
description: 了解如何使用適用於 Azure Data Studio 的機器學習延伸模組，來匯入 ONNX 模型或檢視已經匯入資料庫的模型。
ms.date: 06/09/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3c5faa821ecd9adcfcea426f88a388a6f7d10f27
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901049"
---
# <a name="import-or-view-models-with-machine-learning-extension-preview-for-azure-data-studio"></a>使用適用於 Azure Data Studio 的機器學習延伸模組 (預覽) 匯入或檢視模型

了解如何使用[適用於 Azure Data Studio 的機器學習延伸模組](machine-learning-extension.md)，來匯入 ONNX 模型或檢視已經匯入資料庫的模型。

> [!IMPORTANT]
> 使用機器學習延伸模組，在資料庫中進行匯入和檢視，目前僅支援 [Azure SQL 受控執行個體中的機器學習服務](/azure/azure-sql/managed-instance/machine-learning-services-overview)和[含有 ONNX 的 Azure SQL Edge](/azure/azure-sql-edge/onnx-overview)。

## <a name="prerequisites"></a>必要條件

- 安裝並設定[適用於 Azure Data Studio 的機器學習延伸模組](machine-learning-extension.md)。 您必須[在 [延伸模組設定] 中指定 Python 安裝路徑](machine-learning-extension.md#settings)。

- **onnxruntime**、**mlflow** 及 **mlflow-dbstore** Python 套件。 如果套件尚未安裝，機器學習延伸模組將提示您安裝這些套件。

## <a name="view-models"></a>檢視模型

遵循下列步驟來檢視儲存於資料庫中的 ONNX 模型。

1. 按一下 [匯入或檢視模型]。

1. 如果系統要求您安裝 **onnxruntime**、**mlflow** 及 **mlflow-dbstore**，按一下 [是]。

1. 選取模型儲存所在的**模型資料庫**和**模型資料表**。

這將顯示您的模型清單。 您可以編輯模型名稱與描述，或從清單中刪除模型。

## <a name="import-a-new-model"></a>匯入新模型

遵循下列步驟，在資料庫中匯入 ONNX 模型。

1. 按一下 [匯入或檢視模型]。

1. 如果系統要求您安裝 **onnxruntime**、**mlflow** 及 **mlflow-dbstore**，按一下 [是]。

1. 按一下 [匯入模型]。

1. 選取您想要儲存已匯入模型的**模型資料庫**。

1. 選取您想要儲存已匯入模型的**模型資料表**。 您可以選擇**現有的資料表**，也可以建立**新的資料表**。 按 [下一步] 。

1. 選取模型所在位置，然後按一下 [下一步]。 您可以使用：
    - **檔案上傳**。 選擇此項，以使用檔案中的模型。 選取 [來源檔案] 底下的模型檔案，然後按一下 [下一步]。
    - **Azure Machine Learning**。 選擇此項，以使用來自 Azure Machine Learning 的模型。 首先，**登入 Azure**。 然後，選取您的 **Azure 帳戶**、**Azure 訂用帳戶**、**Azure 資源群組**及 **Azure ML 工作區**。 選取要使用的模型，然後按 [下一步]。

1. 輸入模型**名稱**和**描述**，然後按一下 [部署]，以將模型儲存於您的資料庫中。

> [!NOTE]
> 機器學習延伸模組目前處於預覽狀態。 因此，儲存模型的資料表結構描述可能會在未來變更。

## <a name="next-steps"></a>後續步驟

- [Azure Data Studio 中的機器學習延伸模組](machine-learning-extension.md)
- [管理資料庫中的套件](machine-learning-extension-manage-packages.md)
- [進行預測](machine-learning-extension-predictions.md)
- [SQL 機器學習文件](../machine-learning/index.yml)
- [Azure SQL 受控執行個體中的機器學習服務](/azure/azure-sql/managed-instance/machine-learning-services-overview)
- [SQL Edge (預覽) 中採用 ONNX 的機器學習和 AI](/azure/azure-sql-edge/onnx-overview)
