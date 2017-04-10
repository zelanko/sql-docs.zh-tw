---
title: "Azure Blob 下載工作 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpblobdltask.f1"
  - "sql14.dts.designer.afpblobdltask.f1"
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 12
---
# Azure Blob 下載工作
  Azure Blob 下載工作可讓 SSIS 封裝能從 Azure Blob 儲存體下載檔案。

>   [!NOTE] 為了確保 Azure 儲存體連線管理員及使用它的元件 (也就是 Blob 來源、Blob 目的地、Blob 上傳工作和 Blob 下載工作) 可同時連接到一般目的儲存體帳戶和 Blob 儲存體帳戶，請務必從[這裡](https://www.microsoft.com/download/details.aspx?id=49492)下載最新版的 Azure Feature Pack。 如需這兩種儲存體帳戶類型的詳細資訊，請參閱 [Microsoft Azure 儲存體簡介](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts)。
   
若要加入 **Azure Blob 下載工作**，請將其拖放至 SSIS 設計工具，然後按兩下或按一下滑鼠右鍵，再按一下 [編輯]，即可看到以下 [Azure Blob 下載工作編輯器] 對話方塊。  
  
 **Azure Blob 下載工作**是適用於 SQL Server 2016 的 SQL Server Integration Services (SSIS) Feature Pack for Azure 的元件。 請在 [這裡](http://go.microsoft.com/fwlink/?LinkID=626967)。  
  
 下表提供此對話方塊中欄位的描述。  
  
|||  
|-|-|  
|**欄位**|**說明**|  
|AzureStorageConnection|指定現有的 Azure 儲存體連線管理員，或建立參考 Azure 儲存體帳戶的新連線管理員，而該儲存體帳戶指向裝載 Blob 檔案之處。|  
|BlobContainer|指定包含要下載的 Blob 檔案之 Blob 容器的名稱。|  
|BlobDirectory|指定包含要下載之 Blob 檔案的 Blob 目錄。 Blob 目錄是虛擬的階層式結構。|  
|LocalDirectory|指定將儲存已下載之 Blob 檔案的本機目錄。|  
|FileName|指定名稱篩選，利用指定的名稱模式來選取檔案。 例如  MySheet*.xls\* 包含 MySheet001.xls 及 MySheetABC.xlsx 等檔案。|  
|TimeRangeFrom/TimeRangeTo|指定時間範圍篩選。 將會包含在 **TimeRangeFrom** 之後且 **TimeRangeTo** 之前所修改的檔案。|  
  
  