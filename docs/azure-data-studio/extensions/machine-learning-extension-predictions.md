---
title: 使用機器學習延伸模組進行預測
description: 了解如何使用適用於 Azure Data Studio 的機器學習延伸模組，利用資料庫中的 ONNX 模型進行預測。
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.reviewer: sstein
ms.custom: ''
ms.date: 06/09/2020
ms.openlocfilehash: ad98cd8d9cdeb282a13ff35c278fd1c2a26df2b4
ms.sourcegitcommit: e3460309b301a77d0babec032f53de330da001a9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91136787"
---
# <a name="make-predictions-with-machine-learning-extension-for-azure-data-studio-preview"></a>使用適用於 Azure Data Studio 的機器學習延伸模組 (預覽) 進行預測

了解如何使用[適用於 Azure Data Studio 的機器學習延伸模組](machine-learning-extension.md)，利用資料庫中的 ONNX 模型進行預測。 此延伸模組將使用 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 來產生 T-SQL 指令碼，以利用先前已匯入、位於本機檔案中或來自 Azure Machine Learning 的模型，針對資料表中儲存的資料集進行預測。

> [!IMPORTANT]
> 使用機器學習延伸模組進行預測，目前僅支援 [Azure SQL 受控執行個體中的機器學習服務](/azure/azure-sql/managed-instance/machine-learning-services-overview)和[含有 ONNX 的 Azure SQL Edge](/azure/azure-sql-edge/onnx-overview)。

## <a name="prerequisites"></a>必要條件

- 安裝並設定[適用於 Azure Data Studio 的機器學習延伸模組](machine-learning-extension.md)。 您必須[在 [延伸模組設定] 中指定 Python 安裝路徑](machine-learning-extension.md#settings)。

- **onnxruntime**、**mlflow** 及 **mlflow-dbstore** Python 套件。 如果套件尚未安裝，機器學習延伸模組將提示您安裝這些套件。

## <a name="make-predictions-from-onnx-model"></a>從 ONNX 模型進行預測

遵循下列步驟，以使用 ONNX 模型進行預測。

1. 選取 [進行預測]。

1. 如果系統要求您安裝 **onnxruntime**、**mlflow** 及 **mlflow-dbstore**，請選取 [是]。

1. 選擇模型所在位置，然後選取 [下一步]。 您可以使用：
    - **匯入的模型**。 選擇此項，以使用已經儲存於資料庫中的模型。 選擇模型所在的**模型資料庫**和**模型資料表**、選取要使用的模型，然後選取 [下一步]。
    - **檔案上傳**。 選擇此項，以使用檔案中的模型。 選取 [來源檔案] 底下的模型檔案，然後選取 [下一步]。
    - **Azure Machine Learning**。 選擇此項，以使用來自 Azure Machine Learning 的模型。 首先，**登入 Azure**。 然後，選取您的 **Azure 帳戶**、**Azure 訂用帳戶**、**Azure 資源群組**及 **Azure ML 工作區**。 選取要使用的模型，然後選取 [下一步]。

1. 將來源資料對應至您的模型。
    - 選取包含您要套用預測之資料集的**來源資料庫**和**來源資料表**。
    - 對應 [模型輸入對應] 和 [模型輸出] 底下的資料行。 此延伸模組將自動對應具有相同名稱和資料類型的資料行。

1. 選取 [預測]。

Azure Data Studio 將使用 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 來建立新的 T-SQL 查詢，讓您可用來對資料進行預測。

## <a name="next-steps"></a>後續步驟

- [Azure Data Studio 中的機器學習延伸模組](machine-learning-extension.md)
- [管理資料庫中的套件](machine-learning-extension-manage-packages.md)
- [匯入或檢視模型](machine-learning-extension-import-view-models.md)
- [Azure Data Studio 中的 Notebook](../notebooks-guidance.md)
- [SQL 機器學習文件](../../machine-learning/index.yml)
- [Azure SQL 受控執行個體中的機器學習服務](/azure/azure-sql/managed-instance/machine-learning-services-overview)
- [SQL Edge (預覽) 中採用 ONNX 的機器學習和 AI](/azure/azure-sql-edge/onnx-overview)
