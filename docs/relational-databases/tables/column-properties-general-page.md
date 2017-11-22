---
title: "資料行屬性 (一般頁面) | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.columnproperties.general.f1
ms.assetid: a745890b-994e-4c23-8028-5c83751e60c4
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 141f7fb3b0645ccc32fbee78fa40c403afad5726
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="column-properties-general-page"></a>資料行屬性 (一般頁面)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  使用此頁面來檢視選取之資料行的屬性。  
  
 此頁面的資訊是唯讀的。 若要修改資料行，請關閉 [資料行屬性] 對話方塊，展開物件總管中的資料表和資料行，以滑鼠右鍵按一下資料行，然後按一下 [設計]。  
  
## <a name="options"></a>選項。  
 **名稱**  
 資料行的名稱。  
  
 **資料類型**  
 資料行可保存的資料類型。 如果資料類型是使用者自訂的資料類型，就會顯示使用者自訂資料類型。 如果資料類型不是使用者自訂的資料類型，就會顯示系統資料類型。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。  
  
 **系統類型**  
 資料行可保存的資料類型。 如果資料類型是系統資料類型，就會顯示系統資料類型。 如果資料類型是使用者自訂的資料類型，就會顯示組成使用者自訂資料類型的系統資料類型。  
  
 **主索引鍵**  
 指出資料行是否為主索引鍵。 可能的值為 **True**和 **False**。  
  
 **允許 Null**  
 指出資料行是否接受 Null 值。 可能的值為 **True** 和 **False**。  
  
 **是計算的**  
 指出資料行值是否為計算運算式的結果。  
  
 **計算文字**  
 指出用來計算資料行文字的陳述式。 如需詳細資訊，請參閱 [指定資料表中的計算資料行](../../relational-databases/tables/specify-computed-columns-in-a-table.md)。  
  
 **識別**  
 表示資料行是否為資料表的識別欄位。 可能的值為 **True** 和 **False**。  
  
 **識別種子**  
 指出識別欄位的初始資料列值。  
  
 **識別值增量**  
 [識別值增量] 屬性會指定當 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 為插入的資料列產生識別值時，要加到最大的現有資料列識別值的數值。  
  
 **預設繫結**  
 資料行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設繫結。 若未繫結預設值，此選項可為空白。  
  
 **預設結構描述**  
 識別擁有預設繫結至參考資料行的資料庫結構描述。 若未繫結預設值，此選項可為空白。  
  
 **規則**  
 識別繫結至資料行的資料完整性條件約束。 若未繫結規則，此選項可為空白。  
  
 **規則結構描述**  
 顯示擁有繫結至參考資料行之規則的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫結構描述。 若未繫結規則，此選項可為空白。  
  
 **長度**  
 指出資料行接受的最大字元數或位元組數。  
  
 **定序**  
 顯示資料行的目前定序。 如果空白，將會從物件繼承定序屬性。  
  
 **數值有效位數**  
 指出固定有效位數 (數值資料類型) 的最大位數。  
  
 **數值小數位數**  
 指出固定有效位數 (數值資料類型) 之小數點右邊的位數。  
  
 **XML 結構描述命名空間**  
 以 XML 結構描述定義 (XSD) 語言驗證來定義 XML 資料行的類型。  
  
 **XML 結構描述命名空間結構描述**  
 擁有 XML 結構描述命名空間的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 結構描述。  
  
> [!NOTE]  
>  有數個通用但意義不同的文字結構描述。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用結構描述來組織資料庫物件。 它類似於擁有權。 XML 使用結構描述，將 XML 資訊的組織定義成一系列的命名空間。 這是將相關的 XML 程式碼群組在一起的方法。  
  
 **為疏鬆**  
 指出資料行是否為疏鬆資料行。 可能的值為 **True** 和 **False**。 如需詳細資訊，請參閱 [使用疏鬆資料行](../../relational-databases/tables/use-sparse-columns.md)。  
  
 **是資料行集**  
 指出資料行是否為資料行集。 可能的值為 **True** 和 **False**。 如需詳細資訊，請參閱 [使用資料行集](../../relational-databases/tables/use-column-sets.md)。  
  
 **ANSI 填補狀態**  
 指出開啟或關閉 ANSI 填補。 如需詳細資訊，請參閱 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)。  
  
 **全文檢索**  
 顯示資料行是否參與全文檢索查詢。  
  
 **統計語意**  
 指出此資料行是否啟用統計語意搜尋。 如需詳細資訊，請參閱[語意搜尋 &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md)。  
  
 **不可複寫**  
 指出資料行是否可以複寫。 可能的值為 **True** 和 **False**。  
  
  
