---
title: "使用 OPENROWSET BULK 資料列集提供者大量匯入大型物件資料 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SINGLE_NCLOB option
- bulk rowset providers [SQL Server]
- bulk importing [SQL Server], data formats
- OPENROWSET function, bulk importing large data
- SINGLE_CLOB option
- data formats [SQL Server], large-object data
- large data, bulk imports
- SINGLE_BLOB option
ms.assetid: 171cdd5c-1e47-4bd7-b99a-4f0fd4e10526
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2e2d3cb37032842ca391d4762a990b2808f2c0e
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="bulk-import-large-object-data-with-openrowset-bulk-rowset-provider"></a>使用 OPENROWSET BULK 資料列集提供者大量匯入大型物件資料
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OPENROWSET Bulk 資料列集提供者可讓您將資料檔案當做大型物件資料大量匯入。  
  
 OPENROWSET Bulk 資料列集提供者支援的大型物件資料類型包括 **varbinary**(max) 或 **image**、 **varchar**(max) 或 **text**，以及 **nvarchar**(max) 或 **ntext**。  
  
> [!NOTE]  
>  **image**、 **text** 和 **ntext** 資料類型已被取代。  
  
 OPENROWSET BULK 子句支援三個選項，以單一資料列、單一資料行的資料列集匯入資料檔案的內容。 您可以指定其中一個大型物件選項，而不使用格式檔案。 這些選項如下：  
  
 SINGLE_BLOB  
 將 *data_file* 內容讀取為單一資料列，並以 **varbinary(max)**類型的單一資料行資料列集的形式傳回內容。  
  
 SINGLE_CLOB  
 將指定的資料檔案內容讀取為字元，並使用目前資料庫的定序，以 **varchar(max)**類型的單一資料列、單一資料行資料列集的形式傳回內容；例如文字或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 文件。  
  
 SINGLE_NCLOB  
 將指定的資料檔案內容讀取為 Unicode，並使用目前資料庫的定序，以 **nvarchar(max)**類型的單一資料列、單一資料行資料列集的形式傳回內容。  
  
## <a name="see-also"></a>另請參閱  
 [使用 BULK INSERT 或 OPENROWSET&#40;BULK...&#41; 匯入大量資料 &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [大量匯入期間保留 Null 或使用預設值 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  
