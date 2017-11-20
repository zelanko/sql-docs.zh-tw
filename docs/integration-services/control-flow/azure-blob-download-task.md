---
title: "Azure Blob 下載工作 |Microsoft 文件"
ms.custom: 
ms.date: 07/25/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpblobdltask.f1
- sql14.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 95ea7de4600551cc994e82dd3408cb4ea608685c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="azure-blob-download-task"></a>Azure Blob 下載工作
Azure Blob 下載工作可讓 SSIS 封裝能從 Azure Blob 儲存體下載檔案。

若要加入 **Azure Blob 下載工作**，請將其拖放至 SSIS 設計工具，然後按兩下或在其上按一下滑鼠右鍵，再按一下 [編輯]  ，即可看到以下 [Azure Blob 下載工作編輯器]  對話方塊。  
  
 **Azure Blob 下載工作**是一種元件的[Azure 的 SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。  
  
 下表提供此對話方塊中欄位的描述。  
  
|||  
|-|-|  
|**欄位**|**說明**|  
|AzureStorageConnection|指定現有的 Azure 儲存體連線管理員，或建立參考 Azure 儲存體帳戶的新連線管理員，而該儲存體帳戶指向裝載 Blob 檔案之處。|  
|BlobContainer|指定包含要下載的 Blob 檔案之 Blob 容器的名稱。|  
|BlobDirectory|指定包含要下載之 Blob 檔案的 Blob 目錄。 Blob 目錄是虛擬的階層式結構。|  
|LocalDirectory|指定儲存下載之 blob 檔案的本機目錄。|  
|FileName|指定名稱篩選，利用指定的名稱模式來選取檔案。 例如，`MySheet*.xls\*`包含檔案，例如`MySheet001.xls`和`MySheetABC.xlsx`。|  
|TimeRangeFrom/TimeRangeTo|指定時間範圍篩選。 檔案之後修改**TimeRangeFrom**之前**TimeRangeTo**隨附。|  
  
  

