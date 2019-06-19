---
title: 彈性檔案工作 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPEXTFILETASK.F1
- SQL14.DTS.DESIGNER.AFPEXTFILETASK.F1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2d01304a36f7676f53ffef3f6c6e3c600cb87cb6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66411095"
---
# <a name="flexible-file-task"></a>彈性檔案工作

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

彈性檔案工作讓使用者能夠在各種支援的儲存體服務上執行檔案作業。
以下為目前支援的儲存體服務：

- 本機檔案系統
- [Azure Blob 儲存體](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction) \(部分機器翻譯\)

彈性檔案工作是 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。

若要將彈性檔案工作新增至套件，請將它從 SSIS 工具箱拖曳至設計師畫布。 接著，按兩下該工作，或以滑鼠右鍵按一下該工作並選取 [編輯]  ，以開啟 [彈性檔案工作編輯器]  對話方塊。

**作業**屬性會指定要執行的檔案作業。
目前僅支援**複製**作業。

目前已針對**複製**作業提供下列屬性。

- **SourceConnectionType：** 指定來源連線管理員類型。
- **SourceConnection：** 指定來源連線管理員。
- **SourceFolderPath：** 指定來源資料夾路徑。
- **SourceFileName：** 指定來源檔案名稱。 如果保留空白，將會複製來源資料夾。
- **SearchRecursively：** 指定是否要以遞迴方式複製子資料夾。
- **DestinationConnectionType：** 指定目的地連線管理員類型。
- **DestinationConnection：** 指定目的地連線管理員。
- **DestinationFolderPath：** 指定目的地資料夾路徑。
- **DestinationFileName：** 指定目的地檔案名稱。
