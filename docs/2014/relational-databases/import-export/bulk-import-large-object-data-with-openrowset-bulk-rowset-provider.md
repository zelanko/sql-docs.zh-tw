---
title: 大量匯入大型物件資料使用 OPENROWSET Bulk 資料列集提供者 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f6fe945ea90a150397abecfd83f0ce1c945f217c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012105"
---
# <a name="bulk-import-large-object-data-by-using-the-openrowset-bulk-rowset-provider-sql-server"></a>使用 OPENROWSET BULK 資料列集提供者大量匯入大型物件資料 (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OPENROWSET Bulk 資料列集提供者可讓您將資料檔案當做大型物件資料大量匯入。  
  
 OPENROWSET Bulk 資料列集提供者支援的大型物件資料類型包括 **varbinary**(max) 或 **image**、 **varchar**(max) 或 **text**，以及 **nvarchar**(max) 或 **ntext**。  
  
> [!NOTE]  
>  **image**、 **text** 和 **ntext** 資料類型已被取代。  
  
 OPENROWSET BULK 子句支援三個選項，以單一資料列、單一資料行的資料列集匯入資料檔案的內容。 您可以指定其中一個大型物件選項，而不使用格式檔案。 這些選項如下：  
  
 SINGLE_BLOB  
 將 *data_file* 內容讀取為單一資料列，並以 **varbinary(max)** 類型的單一資料行資料列集的形式傳回內容。  
  
 SINGLE_CLOB  
 將指定的資料檔案內容讀取為字元，並使用目前資料庫的定序，以 **varchar(max)** 類型的單一資料列、單一資料行資料列集的形式傳回內容；例如文字或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word 文件。  
  
 SINGLE_NCLOB  
 將指定的資料檔案內容讀取為 Unicode，並使用目前資料庫的定序，以 **nvarchar(max)** 類型的單一資料列、單一資料行資料列集的形式傳回內容。  
  
## <a name="see-also"></a>另請參閱  
 [使用 BULK INSERT 或 OPENROWSET&#40;BULK...&#41; 匯入大量資料 &#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [大量匯入期間保留 Null 或使用預設值 &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)  
  
  
