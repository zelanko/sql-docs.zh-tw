---
title: Azure Blob 上傳工作 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobuptask.f1
- sql14.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5f5d1d38785cb998ae5f26c62e3de9ff5010c15e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86908442"
---
# <a name="azure-blob-upload-task"></a>Azure Blob 上傳工作

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


「Azure Blob 上傳工作」  可讓 SSIS 封裝將檔案上傳到 Azure Blob 儲存體。
    
若要加入 **Azure Blob 上傳工作**，請將其拖放至 SSIS 設計工具，然後按兩下或在其上按一下滑鼠右鍵，再按一下 [編輯]  ，即可看到以下 [Azure Blob 上傳工作編輯器]  對話方塊。  
  
 **Azure Blob 上傳工作**是 [Azure SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。
  
 下表提供此對話方塊中欄位的描述。  

|**欄位**|**說明**|  
|---|---|  
|AzureStorageConnection|指定現有的 Azure 儲存體連線管理員，或建立參考 Azure 儲存體帳戶的新連線管理員，而該儲存體帳戶指向裝載 Blob 檔案之處。|  
|BlobContainer|指定以 Blob 形式包含上傳之檔案的 Blob 容器名稱。|  
|BlobDirectory|指定以區塊 Blob 形式儲存上傳之檔案的 Blob 目錄。 Blob 目錄是虛擬的階層式結構。 如果在 Blob 已存在，則會遭到取代。|  
|LocalDirectory|指定含有要上傳之檔案的本機目錄。|  
|SearchRecursively|指定是否要以遞迴方式在子目錄中搜尋。|  
|FileName|指定名稱篩選器以選取採用指定名稱模式的檔案。 例如，`MySheet*.xls\*` 包含 `MySheet001.xls` 和 `MySheetABC.xlsx` 等檔案。|  
|TimeRangeFrom/TimeRangeTo|指定時間範圍篩選器。 包含在 **TimeRangeFrom** 之後且 **TimeRangeTo** 之前所修改的檔案。|  
