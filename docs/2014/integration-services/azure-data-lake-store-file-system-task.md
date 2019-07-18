---
title: Azure Data Lake Store 檔案系統工作 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 69a521cb72e68141f5706f5187a0288a3f44f241
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061380"
---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake Store 檔案系統工作

**Azure Data Lake Store 檔案系統工作**可讓使用者在上執行各種不同的檔案系統作業[Azure Data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/)。

若要將 Azure Data Lake Store 檔案系統工作新增至套件，請將它從 SSIS 工具箱拖曳至設計工具畫布。 然後按兩下此工作，或以滑鼠右鍵按一下工作，並選取**編輯**，以開啟 [工作編輯器] 對話方塊。

**Operation** 屬性會指定要執行的檔案系統作業。 支援下列作業。

* **CopyToADLS：** 將檔案上傳到 ADLS。
* **CopyFromADLS：** 從 ADLS 下載檔案。

任何作業都必須指定 Azure Data Lake 連線管理員。

以下是屬性的說明每個作業專屬。

## <a name="copytoadls"></a>CopyToADLS

* **LocalDirectory：** 指定包含要上傳檔案的來源目錄。
* **FileNamePattern：** 指定來源檔案的檔案名稱篩選。 只有其名稱符合指定的模式的檔案將會上傳。 支援萬用字元 `*` 和 `?`。
* **SearchRecursively：** 指定是否要在來源目錄中遞迴搜尋要上傳的檔案。
* **AzureDataLakeDirectory：** 指定要上傳檔案的 ADLS 目的地目錄。
* **FileExpiry：** 指定到期的日期和時間的檔案上傳至 ADLS，或將此屬性保留空白，表示檔案永遠不會過期。

## <a name="copyfromadls"></a>CopyFromADLS

* **AzureDataLakeDirectory：** 指定包含要下載檔案的 ADLS 來源目錄。
* **SearchRecursively：** 指定是否要在來源目錄中遞迴搜尋要下載的檔案。
* **LocalDirectory：** 指定儲存下載檔案的目的地目錄。
