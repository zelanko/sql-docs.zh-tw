---
title: "二進位大型物件 (Blob) 資料 (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-blob"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FILESTREAM [SQL Server], 設計和實作"
ms.assetid: 97509274-c3f8-43e5-a37c-52f1ffe0961a
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 二進位大型物件 (Blob) 資料 (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供在資料庫中或遠端存放裝置上儲存檔案和文件的解決方案。  
  
##  <a name="section"></a> 本節內容  
 [比較用於儲存 Blob 的選項 &#40;SQL Server&#41;](../../relational-databases/blob/compare-options-for-storing-blobs-sql-server.md)  
 比較 FILESTREAM、FileTable 和遠端 Blob 存放區的優點。  
  
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
 FILESTREAM 可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 架構應用程式在檔案系統上儲存非結構化的資料，例如文件和影像。 應用程式可以利用檔案系統的豐富資料流 API 和效能，並同時維護非結構化資料與對應結構化資料之間的交易一致性。  
  
 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
 FileTable 功能可將 Windows 檔案命名空間的支援以及與 Windows 應用程式的相容性提供給儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的檔案資料。 FileTable 可讓應用程式整合其儲存和資料管理元件，並且透過非結構化資料和中繼資料提供整合式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務 (包含全文檢索搜尋和語意搜尋)。  
  
 換句話說，您可以將檔案和文件儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的特殊資料表 (稱為 FileTable) 中，而從 Windows 應用程式存取它們，就像它們儲存在檔案系統中一樣，並不需要對用戶端應用程式進行任何變更。  
  
 [遠端 Blob 存放區 &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
 適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的遠端 BLOB 存放區 (RBS) 可讓資料庫管理員在商品儲存解決方案中儲存二進位大型物件 (BLOB)，而不是直接儲存在伺服器上。 這樣會節省大量的空間，並避免浪費耗費成本的伺服器硬體資源。 RBS 會提供一組 API 程式庫來為應用程式定義標準化模型，以存取 BLOB 資料。 RBS 也包含維護工具 (例如記憶體回收)，以協助管理遠端 BLOB 資料。  
  
 RBS 包含在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝媒體中，但不會由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式安裝。  
  
  