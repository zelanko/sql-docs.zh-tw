---
title: "Azure Blob 上傳工作 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpblobuptask.f1
- sql14.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cec51398ac521abc0345e90b3c6ed156b542b5f1
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="azure-blob-upload-task"></a>Azure Blob 上傳工作
「Azure Blob 上傳工作」可讓 SSIS 封裝將檔案上傳到 Azure Blob 儲存體。
    
若要加入 **Azure Blob 上傳工作**，請將其拖放至 SSIS 設計工具，然後按兩下或在其上按一下滑鼠右鍵，再按一下 [編輯]，即可看到以下 [Azure Blob 上傳工作編輯器] 對話方塊。  
  
 **Azure Blob 上傳工作**是一種元件的[Azure 的 SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。
  
 下表提供此對話方塊中欄位的描述。  
  
|||  
|-|-|  
|**欄位**|**說明**|  
|AzureStorageConnection|指定現有的 Azure 儲存體連線管理員，或建立參考 Azure 儲存體帳戶的新連線管理員，而該儲存體帳戶指向裝載 Blob 檔案之處。|  
|BlobContainer|指定的 blob 容器，其中包含為 blob 上傳的檔案名稱。|  
|BlobDirectory|指定上傳的檔案儲存為區塊 blob 的 blob 目錄。 Blob 目錄是虛擬的階層式結構。 如果 blob 已經存在，則會取代它。|  
|LocalDirectory|指定含有要上傳之檔案的本機目錄。|  
|FileName|指定名稱篩選，利用指定的名稱模式來選取檔案。 例如，`MySheet*.xls\*`包含檔案，例如`MySheet001.xls`和`MySheetABC.xlsx`。|  
|TimeRangeFrom/TimeRangeTo|指定時間範圍篩選。 檔案之後修改**TimeRangeFrom**之前**TimeRangeTo**隨附。|  
  
  

