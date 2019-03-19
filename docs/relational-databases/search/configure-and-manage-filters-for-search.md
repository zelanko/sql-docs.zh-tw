---
title: 設定及管理搜尋的篩選 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0f7d50aac6cea5d7089ee891e533712cc64fd46b
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/18/2019
ms.locfileid: "57973777"
---
# <a name="configure-and-manage-filters-for-search"></a>設定及管理搜尋的篩選
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  編製 **varbinary**、**varbinary(max)**、**image** 或 **xml** 資料類型資料行中文件的索引需要進行額外處理。 這項處理必須由篩選執行。 篩選會從文件中擷取文字資訊 (移除格式)。 然後，篩選會將文字傳送至與資料表資料行相關聯之語言的斷詞工具元件。  
 
## <a name="filters-and-document-types"></a>篩選及文件類型
給定的篩選是給定文件類型 (.doc、.pdf、.xls 和 .xml 等等) 特有的。 這些篩選會實作 IFilter 介面。 如需這些文件類型的詳細資訊，請查詢 [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) 目錄檢視。  
  
二進位文件可以儲存在單一 **varbinary(max)** 或 **image** 資料行中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會根據文件的副檔名，為每個文件選擇正確的篩選。 由於在 **varbinary(max)** 或 **image** 資料行中儲存檔案後，將看不到副檔名，因此必須將副檔名 (.doc、.xls、.pdf 等等) 儲存在資料表的不同資料行中，此資料行稱為類型資料行。 此類型資料行可以是任何一種字元式資料類型，且包含文件副檔名，如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 文件的 .doc。 在 **的** Document [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]資料表中， **Document** 資料行的類型為 **varbinary(max)**，而 **FileExtension**類型資料行的類型為 **nvarchar(8)**。  

**若要檢視現有全文檢索索引中的類型資料行**  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
> [!NOTE]  
>  根據篩選的實作方式，篩選可能會處理父物件中內嵌的物件。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會將篩選設定成遵循其他物件的連結。  

## <a name="installed-filters"></a>安裝的篩選 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會安裝其自有的 XML 和 HTML 篩選。 此外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也會載入已安裝在作業系統上之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 專屬格式 (.doc、.xdoc、.ppt 等) 的篩選。 若要識別目前載入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上的篩選，請使用 [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md) 預存程序，如下所示：  

```sql
EXEC sp_help_fulltext_system_components 'filter';   
```  

> [!NOTE]
> 即使有提供 .xlsx 支援的最新版 Office Filter Pack，SQL Server 還是無法支援 Strict Open XML 試算表。  SQL Server 會直接在編製任何 Strict Open XML 試算表的內容索引時失敗，而不會傳回任何錯誤。

## <a name="non-microsoft-filters"></a>非 Microsoft 篩選
不過，您必須先手動將非 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 格式的篩選載入伺服器執行個體中，才能加以使用。 如需安裝其他篩選的相關資訊，請參閱 [檢視或變更已註冊的篩選與斷詞工具](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)。  
  
  
## <a name="see-also"></a>另請參閱  
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [FILESTREAM 與其他 SQL Server 功能的相容性](../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
