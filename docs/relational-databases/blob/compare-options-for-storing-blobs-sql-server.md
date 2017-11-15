---
title: "比較用於儲存 Blob 的選項 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6038697b-36a9-49e8-a02a-2ad9e2e60e5a
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1cc4faaa92e5e42ce16f385e7d9e9a3a87c65a2e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="compare-options-for-storing-blobs-sql-server"></a>比較用於儲存 Blob 的選項 (SQL Server)
  討論和比較 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中儲存檔案和文件的可用選項。  
  
##  <a name="Expectations"></a> 在資料庫中儲存檔案 - 優點和期望  
 大部分企業資料的本質都是非結構化，而且通常會在檔案系統中儲存成檔案和文件。 其中大多數資料是由透過 Windows API 存取檔案的應用程式所產生、管理和取用。 企業通常會將這項資料保存在檔案系統中，而將檔案的相關中繼資料儲存在關聯式資料庫中。  
  
 將非結構化資料整合至關聯式資料庫，提供重要的優點。 這些優點包括：  
  
-   整合式儲存和資料管理功能，例如備份。  
  
-   整合式服務，例如針對資料和中繼資料進行全文檢索搜尋和語意搜尋。  
  
-   輕易地針對非結構化資料進行管理和原則管理。  
  
 不過，在大部分情況下，將非結構化資料儲存在關聯式資料庫中並不是那麼方便。 先前一直無法在關聯式系統上執行以 Windows 為基礎的現有應用程式。 將已建立的應用程式 (例如 Microsoft Word 或 Adobe Reader) 重寫成可在關聯式資料庫 API 上執行並不實用。 這些應用程式只期望能夠透過 Windows API 存取資料。 換言之，這些期望包括：  
  
-   Windows 應用程式無法識別資料庫交易而且不需要它們。  
  
-   Windows 應用程式需要與檔案和目錄資料的檔案系統 API 相容。  
  
##  <a name="Filestream"></a> FILESTREAM  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已經具有 FILESTREAM 功能，可針對在檔案系統上儲存成檔案的非結構化資料提供有效率的儲存、管理及資料流處理。 不過，FILESTREAM 解決方案需要自訂程式設計，因此無法滿足上述完整 Windows 應用程式相容性的需求。  
  
##  <a name="FileTables"></a> FileTable  
 FileTable 功能是以現有的 FILESTREAM 功能為建置基礎，透過處理檔案架構資料之非交易式存取和 Windows 應用程式相容性的需求，讓企業客戶能夠在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中儲存非結構化檔案資料和目錄階層。  
  
##  <a name="CompareFileTable"></a> 比較 FILESTREAM 與 FileTable  
  
|功能|檔案伺服器和資料庫解決方案|FILESTREAM 解決方案|FileTable 解決方案|  
|-------------|---------------------------------------|-------------------------|------------------------|  
|**管理工作的單一本文**|否|是|**是**|  
|**單一服務集合**：搜尋、報表、查詢等等|否|是|**是**|  
|**整合式安全性模型**|否|是|**是**|  
|**FILESTREAM 資料的就地更新**|是|否|**是**|  
|**在資料庫中維護的檔案和目錄階層**|否|否|**是**|  
|**Windows 應用程式相容性**|是|否|**是**|  
|**檔案屬性的關聯式存取**|否|否|**是**|  
  
##  <a name="CompareRBS"></a> 比較 FILESTREAM 與遠端 BLOB 存放區 (RBS)  
 如需此兩種功能的比較，請參閱 RBS 小組的這篇部落格文章： [SQL Server 遠端 BLOB 存放區和 FILESTREAM 功能比較](http://go.microsoft.com/fwlink/?LinkId=210317)。  
  
##  <a name="more"></a> 其他資訊  
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
 [遠端 Blob 存放區 &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
