---
title: 實作 DDL 觸發程序 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL triggers, implementing
ms.assetid: f44e5340-1d18-40e9-828e-0ffcca091ae3
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 60fd6f077d94e1d39cd7ae6c006d92f3d50ec9af
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424097"
---
# <a name="implement-ddl-triggers"></a>實作 DDL 觸發程序
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  本主題提供資訊以協助您建立 DDL 觸發程式、修改 DDL 觸發程式並停用或卸除 DDL 觸發程式。  
  
## <a name="creating-ddl-triggers"></a>建立 DDL 觸發程序  
 您可以使用 DDL 觸發程序的 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TRIGGER 陳述式，建立 DDL 觸發程序。  
  
 **建立 DDL 觸發程序**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
> [!IMPORTANT]  
>  從觸發程序傳回結果集的功能，將會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]未來的版本中移除。 傳回結果集的觸發程序可能會導致非專用的應用程式發生非預期的行為。 請在新的開發工作中避免從觸發程序傳回結果集，並計畫修改目前如此運作的應用程式。 若要避免在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中從觸發程序傳回結果集，請將 [不允許來自觸發程序的結果選項](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) 設為 1。 在未來版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，此選項的預設值會是 1。  
  
## <a name="modifying-ddl-triggers"></a>修改 DDL 觸發程序  
 如果您必須修改 DDL 觸發程序的定義，您可以卸除觸發程序後重新加以建立，或是在單一步驟中重新定義現有的觸發程序。  
  
 如果您變更 DDL 觸發程序所參考的物件名稱，就必須修改觸發程序使其文字反映新名稱。 因此，在改變物件名稱時，首先要檢視此物件的相依性以判斷是否有相關的觸發程序受到影響。  
  
 您也可以將觸發程序的定義修改為加密的形態。  
  
 **修改觸發程序**  
  
-   [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
 **檢視觸發程序的相依性**  
  
-   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
-   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)  
  
-   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
## <a name="disabling-and-dropping-ddl-triggers"></a>停用和卸除 DDL 觸發程序  
 不再需要 DDL 觸發程序時，可以將它停用或刪除。  
  
 停用 DDL 觸發程序不會將它卸除。 該觸發程序仍然會以物件形式存在於目前的資料庫中。 不過，只要編寫它的任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式在執行時，觸發程序就不會引發。 已停用的 DDL 觸發程序可重新啟用。 啟用 DDL 觸發程序會讓它以原先建立時相同的方式引發。 建立 DDL 觸發程序時，預設是啟用的。  
  
 刪除 DDL 觸發程序時，會從目前的資料庫卸除。 DDL 觸發程序所參考的任何物件或資料都不會受到影響。  
  
 **停用 DDL 觸發程序**  
  
-   [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
 **啟用 DDL 觸發程序**  
  
-   [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
 **刪除 DDL 觸發程序**  
  
-   [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)  
  
  
