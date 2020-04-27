---
title: 取得元件的相關資訊 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], metadata
- status information [SQL Server], assemblies
- metadata [SQL Server], assemblies
ms.assetid: 6aa7f18e-baad-4481-9777-8c3b230b392f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ebbb5ac25ea71dc5b9929fb529414b059c0589fb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62919299"
---
# <a name="getting-information-about-assemblies"></a>取得組件的相關資訊
  您可以查詢下列的目錄檢視及函數，以取得組件的相關中繼資料。  
  
 **若要取得個別組件的相關資訊**  
  
-   [ASSEMBLYPROPERTY &#40;Transact-sql&#41;](/sql/t-sql/functions/assemblyproperty-transact-sql)  
  
 **若要取得資料庫中所有組件的相關資訊**  
  
-   [sys.databases &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-assemblies-transact-sql)  
  
 **若要取得組件檔案的相關資訊，包括組件二進位、來源檔案及偵錯檔案**  
  
-   [assembly_files &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-files-transact-sql)  
  
 **若要取得跨組件參考的相關資訊**  
  
-   [assembly_references &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-references-transact-sql)  
  
 **若要取得使用者定義型別的相關組件資訊**  
  
-   [assembly_types &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-types-transact-sql)  
  
-   [sys.types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-types-transact-sql)  
  
 **若要取得 Common Language Runtime (CLR) 預存程序、觸發程序及函數的相關組件資訊**  
  
-   [sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)  
  
 **若要取得非 CLR 物件的相關資訊**  
  
-   [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)  
  
## <a name="see-also"></a>另請參閱  
 [元件 &#40;資料庫引擎&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [設計元件](../../relational-databases/clr-integration/assemblies-designing.md)   
 [實作組件](assemblies-implementing.md)  
  
  
