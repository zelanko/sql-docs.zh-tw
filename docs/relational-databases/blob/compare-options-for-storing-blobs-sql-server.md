---
title: 比較用於儲存 Blob 的選項 (SQL Server) | Microsoft Docs
description: SQL Server 可儲存 Windows 應用程式所使用的二進位大型物件 (Blob) 資料。 比較此關聯式資料庫中用於儲存非結構化資料的選項。
ms.custom: ''
ms.date: 03/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
ms.assetid: 6038697b-36a9-49e8-a02a-2ad9e2e60e5a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7b0faae244963957eadb1bd894f90a88736427b4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768061"
---
# <a name="compare-options-for-storing-blobs-sql-server"></a>比較用於儲存 Blob 的選項 (SQL Server)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

討論和比較 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中儲存檔案和文件的可用選項。

## <a name="storing-files-in-the-database---benefits-and-expectations"></a><a name="Expectations"></a> 在資料庫中儲存檔案 - 優點和期望

大部分企業資料的本質都是非結構化，而且通常會在檔案系統中儲存成檔案和文件。 其中大多數資料是由透過 Windows API 存取檔案的應用程式所產生、管理和取用。 企業通常會將這項資料保存在檔案系統中，而將檔案的相關中繼資料儲存在關聯式資料庫中。

將非結構化資料整合至關聯式資料庫，可帶來下列優點：

- 整合式儲存和資料管理功能，例如備份。
- 整合式服務，例如針對資料和中繼資料進行全文檢索搜尋和語意搜尋。
- 輕易地針對非結構化資料進行管理和原則管理。

要在關聯式資料庫中儲存非結構化資料，向來很不方便。 重寫已建立好的應用程式 (例如 Microsoft Word 或 Adobe Reader) 以透過關聯式資料庫 API 互動，是不實際的做法。 這些應用程式期望能夠透過 Windows API 存取資料。 應用程式的預期如下：

- Windows 應用程式無法識別資料庫交易而且不需要它們。
- Windows 應用程式需要與檔案和目錄資料的檔案系統 API 相容。

多年前，SQL Server 並未提供任何一種可在關聯式資料庫中儲存非結構化資料的方式。 但現在，確實有方法可以儲存非結構化資料了。

## <a name="filestream"></a><a name="Filestream"></a> FILESTREAM

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已經有 FILESTREAM 功能。 FILESTREAM 功能為在檔案系統上儲存成檔案的非結構化資料，提供有效率的儲存、管理及資料流處理。 不過，FILESTREAM 解決方案需要自訂程式設計，因此無法滿足上述完整 Windows 應用程式相容性的需求。

## <a name="filetables"></a><a name="FileTables"></a> FileTable

FileTable 功能建基於現有的 FILESTREAM 功能。 FileTable 功能可讓企業客戶在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中儲存非結構化檔案資料，以及目錄階層。 這項功能解決了檔案型資料的非交易式存取及 Windows 應用程式相容性問題。

## <a name="comparing-filestream-and-filetable"></a><a name="CompareFileTable"></a> 比較 FILESTREAM 與 FileTable

|功能|檔案伺服器和資料庫解決方案|FILESTREAM 解決方案|FileTable 解決方案|
|:------|:--------------------------------|:------------------|:-----------------|
|**管理工作的單一本文**|否|是|**是**|
|**單一服務集合**：搜尋、報表、查詢等等|否|是|**是**|
|**整合式安全性模型**|否|是|**是**|
|**FILESTREAM 資料的就地更新**|是|否|**是**|
|**在資料庫中維護的檔案和目錄階層**|否|否|**是**|
|**Windows 應用程式相容性**|是|否|**是**|
|**檔案屬性的關聯式存取**|否|否|**是**|

## <a name="comparing-filestream-and-remote-blob-store-rbs"></a><a name="CompareRBS"></a> 比較 FILESTREAM 與遠端 BLOB 存放區 (RBS)

儲存非結構化資料的另一個選項是遠端 BLOB 存放區 (RBS)。 如需詳細資訊，請參閱[遠端 BLOB 存放區 (RBS) (SQL Server)](remote-blob-store-rbs-sql-server.md)。

## <a name="more-information"></a><a name="more"></a> 其他資訊

[FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
[遠端 Blob 存放區 &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)
