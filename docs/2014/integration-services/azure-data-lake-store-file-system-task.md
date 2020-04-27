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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66061380"
---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake Store 檔案系統工作

**Azure Data Lake 儲存區檔案系統**工作可讓使用者在[Azure Data Lake 存放區（ADLS）](https://azure.microsoft.com/services/data-lake-store/)上執行各種檔案系統作業。

若要將 Azure Data Lake Store 檔案系統工作新增至套件，請將它從 SSIS 工具箱拖曳至設計工具畫布。 然後按兩下該工作，或以滑鼠右鍵按一下工作並選取 [**編輯**]，以開啟 [工作編輯器] 對話方塊。

**Operation** 屬性會指定要執行的檔案系統作業。 支援下列作業。

* **CopyToADLS：** 將檔案上傳至 ADLS。
* **CopyFromADLS：** 從 ADLS 下載檔案。

任何作業都必須指定 Azure Data Lake 連線管理員。

以下是每個作業特定屬性的描述。

## <a name="copytoadls"></a>CopyToADLS

* **LocalDirectory：** 指定包含要上傳之檔案的來原始目錄。
* **FileNamePattern：** 指定來源檔案的檔案名稱篩選。 只會上傳名稱符合指定模式的檔案。 支援萬用字元 `*` 和 `?`。
* **SearchRecursively：** 指定是否以遞迴方式在要上傳檔案的來源目錄中搜尋。
* **AzureDataLakeDirectory：** 指定檔案上傳位置的 ADLS 目的地目錄。
* **FileExpiry：** 指定要上傳至 ADLS 之檔案的到期日期和時間，或將此屬性保留空白，表示檔案永不過期。

## <a name="copyfromadls"></a>CopyFromADLS

* **AzureDataLakeDirectory：** 指定包含要下載檔案的 ADLS 來源目錄。
* **SearchRecursively：** 指定是否以遞迴方式在要下載檔案的來源目錄中搜尋。
* **LocalDirectory：** 指定儲存下載檔案的目的地目錄。
