---
title: 升級之後，新的保留關鍵字不能當做識別碼使用 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- keywords [SQL Server], after upgrade
- keywords [SQL Server], reserved
- keywords [SQL Server]
ms.assetid: cb242081-54f8-4273-a8ef-52f3751c25ef
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d187fbe95a75091b0cbcf4bf09225c5f60a9af01
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66096884"
---
# <a name="after-upgrade-new-reserved-keywords-cannot-be-used-as-identifiers"></a>升級之後無法將保留關鍵字當做識別碼
  Upgrade Advisor 偵測到有使用保留關鍵字。 保留關鍵字無法當做識別碼或物件名稱使用，除非您分隔此名稱。  
  
## <a name="component"></a>元件  
 Database Engine  
  
## <a name="description"></a>描述  
 在 90 或低於 90 的相容性層級上，以下字不是保留關鍵字，而且不能當做 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼中的識別碼或物件名稱。 在相容性層級 100 上，這些字是完整保留關鍵字，而且不應該當做識別碼或物件名稱使用。  
  
-   EXTERNAL  
  
-   MERGE  
  
-   PIVOT  
  
-   REVERT  
  
-   STOPLIST  
  
-   TABLESAMPLE  
  
-   UNPIVOT  
  
## <a name="corrective-action"></a>更正動作  
 我們建議您重新命名物件。 如果您無法在升級之前完成此動作，請使用下列其中一種方法，直到能夠變更名稱為止：  
  
-   保留資料庫相容性層級設定 90 或更低。  
  
-   使用分隔識別碼來參考物件。 例如，語句`CREATE TABLE [MERGE] ([MERGE] int);`會使用括弧來分隔物件名稱 MERGE。  
  
## <a name="external-resources"></a>外部資源  
 [&#40;Transact-sql&#41;的保留關鍵字](/sql/t-sql/language-elements/reserved-keywords-transact-sql)  
  
 [MERGE &#40;Transact-SQL&#41;](/sql/t-sql/statements/merge-transact-sql)  
  
 [分隔識別碼 (Database Engine)](https://go.microsoft.com/fwlink/?LinkId=112509)  
  
 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
