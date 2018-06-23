---
title: 設定及管理搜尋的篩選 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
caps.latest.revision: 68
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ccafb0bccab01286534a0c5499fe474da1262d5d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036082"
---
# <a name="configure-and-manage-filters-for-search"></a>設定及管理搜尋的篩選
  索引中的文件`varbinary`， `varbinary(max)`， `image`，或`xml`資料類型資料行需要進行額外處理。 這項處理必須由篩選執行。 篩選會從文件中擷取文字資訊 (移除格式)。 然後，篩選會將文字傳送至與資料表資料行相關聯之語言的斷詞工具元件。  
  
 給定的篩選是給定文件類型 (.doc、.pdf、.xls 和 .xml 等等) 特有的。 這些篩選會實作 IFilter 介面。 如需這些文件類型的詳細資訊，請查詢 [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) 目錄檢視。  
  
 二進位文件可以儲存在單一 `varbinary(max)` 或 `image` 資料行中。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會根據文件的副檔名，為每個文件選擇正確的篩選。 因為看不到副檔名當檔案儲存在`varbinary(max)`或`image`必須在稱為類型資料行的資料表中的個別資料行中儲存資料行中，檔案的副檔名 （.doc、.xls、.pdf 等等）。 此類型資料行可以是任何一種字元式資料類型，且包含文件副檔名，如 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Word 文件的 .doc。 在**文件**資料表中[!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]、**文件**資料行是類型`varbinary(max)`，和型別資料行**FileExtension**，屬於類型`nvarchar(8)`。  
  
> [!NOTE]  
>  根據篩選的實作方式，篩選可能會處理父物件中內嵌的物件。 不過， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會將篩選設定成遵循其他物件的連結。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會安裝其自有的 XML 和 HTML 篩選。 此外， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 也會載入已經安裝在作業系統上的其他任何  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]專用格式 (.doc、.xdoc、.ppt 等等) 篩選。 若要識別目前載入到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體上的篩選，請使用 [sp_help_fulltext_system_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql) 預存程序，如下所示：  
  
```  
EXEC sp_help_fulltext_system_components 'filter';   
```  
  
 不過，您必須先手動將非 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 格式的篩選載入伺服器執行個體中，然後才能使用它們。 如需安裝其他篩選的相關資訊，請參閱 [檢視或變更已註冊的篩選與斷詞工具](view-or-change-registered-filters-and-word-breakers.md)。  
  
 **若要檢視現有全文檢索索引中的類型資料行**  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
## <a name="see-also"></a>另請參閱  
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)   
 [FILESTREAM 與其他 SQL Server 功能的相容性](../blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
