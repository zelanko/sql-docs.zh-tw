---
title: Azure Data Lake Store 檔案系統工作 | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: Lingxi-Li
ms.author: lingxl
ms.reviewer: maghan
ms.openlocfilehash: f5cd88953a9f33fa4ba44784d30333487a8d832b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763639"
---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake Store 檔案系統工作

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Azure Data Lake Store 檔案系統工作讓使用者在 [Azure Data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/) 上執行各種不同的檔案系統作業。

Azure Data Lake Store 檔案系統工作是 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。

## <a name="configure-the-azure-data-lake-store-file-system-task"></a>設定 Azure Data Lake Store 檔案系統工作

若要將 Azure Data Lake Store 檔案系統工作新增至套件，請將它從 SSIS 工具箱拖曳至設計工具畫布。 然後按兩下工作，或按一下滑鼠右鍵選取 [編輯]  ，開啟 [Azure Data Lake Store File System Task Editor] (Azure Data Lake Store 檔案系統工作編輯器)  對話方塊。

**Operation** 屬性會指定要執行的檔案系統作業。 選取下列作業的其中之一：

- **CopyToADLS：** 將檔案上傳至 ADLS。
- **CopyFromADLS：** 從 ADLS 下載檔案。

## <a name="configure-the-properties-for-the-operation"></a>設定作業的屬性
任何作業都必須指定 Azure Data Lake 連線管理員。

以下是每一項作業的專用屬性：

### <a name="copytoadls"></a>CopyToADLS
- **LocalDirectory：** 指定包含要上傳檔案的本機來源目錄。
- **FileNamePattern：** 指定來源檔案的檔案名稱篩選。 只上傳名稱符合指定模式的檔案。 支援萬用字元 `*` 和 `?`。
- **SearchRecursively：** 指定是否以遞迴方式在要上傳檔案的來源目錄中搜尋。
- **AzureDataLakeDirectory：** 指定檔案上傳位置的 ADLS 目的地目錄。
- **FileExpiry：** 指定檔案上傳至 ADLS 的到期日期和時間。 此屬性留白表示檔案永遠不過期。

### <a name="copyfromadls"></a>CopyFromADLS
- **AzureDataLakeDirectory：** 指定包含要下載檔案的 ADLS 來源目錄。
- **SearchRecursively：** 指定是否以遞迴方式在要下載檔案的來源目錄中搜尋。
- **LocalDirectory：** 指定儲存下載檔案的目的地目錄。
