---
title: "Azure Blob 來源 | Microsoft Docs"
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
  - "sql13.dts.designer.afpblobsrc.f1"
  - "sql14.dts.designer.afpblobsrc.f1"
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Azure Blob 來源
  **Azure Blob 來源**元件可讓 SSIS 封裝從 Azure Blob 讀取資料。 支援的檔案格式：CSV 與 AVRO。
  
>   [!NOTE] 為了確保 Azure 儲存體連線管理員及使用它的元件 (也就是 Blob 來源、Blob 目的地、Blob 上傳工作和 Blob 下載工作) 可同時連接到一般目的儲存體帳戶和 Blob 儲存體帳戶，請務必從[這裡](https://www.microsoft.com/download/details.aspx?id=49492)下載最新版的 Azure Feature Pack。 如需這兩種儲存體帳戶類型的詳細資訊，請參閱 [Microsoft Azure 儲存體簡介](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts)。
  
  若要查看 Azure Blob 來源的編輯器，可在資料流程設計師上拖放 **Azure Blob 來源**，並連按兩下以開啟編輯器。  
  
 **Azure Blob 來源**是適用於 SQL Server 2016 之 Azure SQL Server Integration Services (SSIS) 功能套件的元件。 請在 **這裡**。  
  
1.  針對 [Azure 儲存體連線管理員] 欄位，請指定現有的 Azure 儲存體連線管理員，或建立參考 Azure 儲存體帳戶的新連線管理員。  
  
2.  針對 [Blob 容器名稱] 欄位，請指定包含原始程式檔的 Blob 容器名稱。  
  
3.  針對 [Blob 名稱] 欄位，請指定 Blob 的路徑。  
  
4.  針對 [Blob 檔案格式] 欄位，請指定要使用的 Blob 格式。  
  
5.  若檔案格式為 CSV，則您必須指定 [資料行分隔符號字元] 值。 若檔案中第一個資料列包含資料行名稱，請選取 [第一個資料列的資料行名稱]。  
  
6.  指定連接資訊後，請切換至 [資料行] 頁面，將來源資料行對應至 SSIS 資料流程的目的地資料行。  
  
  