---
title: Azure Blob 上傳工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobuptask.f1
- sql11.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 392fcbf3a46b48b2032b5792321e9a22b3027341
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832773"
---
# <a name="azure-blob-upload-task"></a>Azure Blob 上傳工作
  Azure Blob 上傳工作可讓 SSIS 封裝將檔案上傳至 Azure blob 儲存體。   
若要加入 **Azure Blob 上傳工作**，請將其拖放至 SSIS 設計工具，然後按兩下或在其上按一下滑鼠右鍵，再按一下 [編輯]，即可看到以下 [Azure Blob 上傳工作編輯器] 對話方塊。  
  
 下表提供此對話方塊中欄位的描述。  
  
|||  
|-|-|  
|**欄位**|**說明**|  
|AzureStorageConnection|指定現有的 Azure 儲存體連線管理員，或建立參考 Azure 儲存體帳戶的新連線管理員，而該儲存體帳戶指向裝載 Blob 檔案之處。|  
|BlobContainer|指定以 Blob 形式保存上傳之檔案的 Blob 容器名稱。|  
|BlobDirectory|指定以區塊 Blob 形式儲存上傳之檔案的 Blob 目錄。 Blob 目錄是虛擬的階層式結構。 如果在 Blob 已存在，將會遭到取代。|  
|LocalDirectory|指定含有要上傳之檔案的本機目錄。|  
|FileName|指定名稱篩選，利用指定的名稱模式來選取檔案。 例如 MySheet*.xls\* 包含 MySheet001.xls 及 MySheetABC.xlsx 等檔案。|  
|TimeRangeFrom/TimeRangeTo|指定時間範圍篩選。 將會包含在 **TimeRangeFrom** 之後且 **TimeRangeTo** 之前所修改的檔案。|  
  
  
