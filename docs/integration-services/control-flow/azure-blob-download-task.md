---
title: Azure Blob 下載工作 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobdltask.f1
- sql14.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fc83e4d8e39c5521fd897ceeec07755f62b5765d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294321"
---
# <a name="azure-blob-download-task"></a>Azure Blob 下載工作

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Azure Blob 下載工作可讓 SSIS 封裝能從 Azure Blob 儲存體下載檔案。

若要加入 **Azure Blob 下載工作**，請將其拖放至 SSIS 設計工具，然後按兩下或按一下滑鼠右鍵，再按一下 [編輯]  ，即可看到以下 [Azure Blob 下載工作編輯器]  對話方塊。  
  
 **Azure Blob 下載工作**是 [Azure SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。  
  
 下表提供此對話方塊中欄位的描述。  

|**欄位**|**說明**|  
|---|---|
|AzureStorageConnection|指定現有的 Azure 儲存體連線管理員，或建立參考 Azure 儲存體帳戶的新連線管理員，而該儲存體帳戶指向裝載 Blob 檔案之處。|  
|BlobContainer|指定包含要下載的 Blob 檔案之 Blob 容器的名稱。|  
|BlobDirectory|指定包含要下載之 Blob 檔案的 Blob 目錄。 Blob 目錄是虛擬的階層式結構。|  
|SearchRecursively|指定是否要以遞迴方式在子目錄中搜尋。|  
|LocalDirectory|指定儲存已下載之 Blob 檔案的本機目錄。|  
|FileName|指定名稱篩選器以選取採用指定名稱模式的檔案。 例如，`MySheet*.xls\*` 包含 `MySheet001.xls` 和 `MySheetABC.xlsx` 等檔案。|  
|TimeRangeFrom/TimeRangeTo|指定時間範圍篩選器。 包含在 **TimeRangeFrom** 之後且 **TimeRangeTo** 之前所修改的檔案。|  
