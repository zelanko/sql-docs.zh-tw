---
title: "Azure Data Lake Store 檔案系統工作 |Microsoft 文件"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: douglasl
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: cbc72958f992e0b5cae12cdfc8c0996378f9708c
ms.contentlocale: zh-tw
ms.lasthandoff: 10/11/2017

---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake Store 檔案系統工作

Azure 資料湖存放區檔案系統工作可讓使用者執行各種不同的檔案系統作業上[Azure 資料湖存放區 (ADLS)](https://azure.microsoft.com/services/data-lake-store/)。

Azure 資料湖存放區檔案系統工作是一種元件的[Azure 的 SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。

## <a name="configure-the-azure-data-lake-store-file-system-task"></a>設定 Azure Data Lake Store 檔案系統工作

若要將 Azure 資料湖存放區檔案系統 」 工作加入封裝時，將它從 [SSIS 工具箱] 拖曳至設計工具的畫布。 按兩下此工作，或以滑鼠右鍵按一下工作，然後選取**編輯**，以開啟**Azure 資料湖存放區檔案系統工作編輯器** 對話方塊。

**作業**屬性會指定要執行的檔案系統作業。 選取下列作業之一：

- **CopyToADLS:**檔案上傳至 ADLS。
- **CopyFromADLS:**從 ADLS 下載檔案。

## <a name="configure-the-properties-for-the-operation"></a>設定作業的屬性
對於任何作業，您必須指定 Azure 資料湖連接管理員。

以下是屬性特定的每一項作業：

### <a name="copytoadls"></a>CopyToADLS
- **LocalDirectory:**指定含有要上傳檔案的本機來源目錄。
- **FileNamePattern:**指定原始程式檔的檔案名稱篩選條件。 上傳其名稱符合指定的模式的檔案。 萬用字元`*`和`?`支援。
- **SearchRecursively:**指定是否要搜尋以遞迴方式上傳檔案的來源目錄內。
- **AzureDataLakeDirectory:**指定檔案上傳到的 ADLS 目的地目錄。
- **FileExpiry:**指定到期的日期和時間的檔案上傳至 ADLS。 將此屬性保留空白，表示檔案永遠不過期。

### <a name="copyfromadls"></a>CopyFromADLS
- **AzureDataLakeDirectory:**指定包含要下載之檔案的 ADLS 來源目錄。
- **SearchRecursively:**指定是否要下載的檔案的來源目錄中以遞迴方式搜尋。
- **LocalDirectory:**指定要儲存下載的檔案的目的地目錄。

