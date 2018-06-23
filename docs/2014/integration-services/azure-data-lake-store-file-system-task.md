---
title: Azure Data Lake Store 檔案系統工作 | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
caps.latest.revision: 3
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.openlocfilehash: 240780efd1b12596b0ebb6156ad98c508f0e8051
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022200"
---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake Store 檔案系統工作
**Azure 資料湖存放區檔案系統工作**可讓使用者執行各種不同的檔案系統作業上[Azure 資料湖存放區 (ADLS)](https://azure.microsoft.com/en-us/services/data-lake-store/)。

若要將 Azure Data Lake Store 檔案系統工作新增至套件，請將它從 SSIS 工具箱拖曳至設計工具畫布。 按兩下此工作，或以滑鼠右鍵按一下工作，然後選取**編輯**，以開啟 [工作編輯器] 對話方塊。

**Operation** 屬性會指定要執行的檔案系統作業。 支援下列作業。

* **CopyToADLS：** 將檔案上傳至 ADLS。
* **CopyFromADLS：** 從 ADLS 下載檔案。

任何作業都必須指定 Azure Data Lake 連線管理員。

以下是屬性的說明每個作業專屬。

## <a name="copytoadls"></a>CopyToADLS
* **LocalDirectory:** 指定含有要上傳檔案的來源目錄。
* **FileNamePattern：** 指定來源檔案的檔案名稱篩選。 將會上傳其名稱符合指定的模式的檔案。 支援萬用字元 `*` 和 `?`。
* **SearchRecursively：** 指定是否以遞迴方式在要上傳檔案的來源目錄中搜尋。
* **AzureDataLakeDirectory：** 指定檔案上傳位置的 ADLS 目的地目錄。
* **FileExpiry:** 指定到期的日期和時間的檔案上傳至 ADLS，或將此屬性保留空白，表示檔案永遠不過期。

## <a name="copyfromadls"></a>CopyFromADLS
* **AzureDataLakeDirectory：** 指定包含要下載檔案的 ADLS 來源目錄。
* **SearchRecursively：** 指定是否以遞迴方式在要下載檔案的來源目錄中搜尋。
* **LocalDirectory：** 指定儲存下載檔案的目的地目錄。
