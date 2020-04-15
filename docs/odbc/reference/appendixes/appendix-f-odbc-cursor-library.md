---
title: 附錄 F:ODBC 游標庫 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec7982150bfa805c7093ab445400ef5ad1ee070c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292428"
---
# <a name="appendix-f-odbc-cursor-library"></a>附錄 F：ODBC 資料指標程式庫
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 ODBC 遊標庫 (Odbccr32.dll) 支援符合 1 級 API 符合性級別且開發人員可以使用其應用程式或驅動程式重新分發的任何驅動程式的可滾動遊標。 游標庫還支援**為 SELECT**語句生成的結果集定位更新和刪除語句。 儘管它僅支持靜態和僅轉發遊標,但游標庫可滿足許多應用程式的需求。 此外,它可以提供良好的性能,特別是對於中小型結果集,以及沒有良好游標支援的應用程式。  
  
 游標庫是位於驅動程式管理器和驅動程式之間的動態連結庫 (DLL)。 當應用程式呼叫函數時,驅動程式管理員呼叫游標庫中的函數,該庫執行該函數或在指定的驅動程式中呼叫該函數。 對於給定的連接,應用程式指定是否始終使用游標庫、驅動程式不支援可滾動遊標或從未使用過。  
  
 游標庫顯示為驅動程式管理器的驅動程式。 如果游標庫位於驅動程式管理員和 ODBC *2.x*驅動程式之間,則游標庫將顯示為 ODBC *2.x*驅動程式。 如果游標庫位於驅動程式管理員和 ODBC *3.x*驅動程式之間,則游標庫顯示為 ODBC *3.x*驅動程式。 游標庫顯示的行為取決於它使用的驅動程式的版本,但綁定偏移量除外,ODBC *2.x*和 ODBC *3.x*驅動程式都支援該偏移量。  
  
 為了在**SQLFetch**和**SQLFetchScroll**中實現塊游標,遊標庫在驅動程式中反覆調用**SQLFetch。** 為了實現滾動,它緩存它在記憶體和磁碟檔中檢索的數據。 當應用程式請求新的行集時,游標庫根據需要從驅動程式或緩存中檢索它。  
  
 要實現定位的更新和刪除語句,游標庫構造一個**更新**或**DELETE**語句,該語句具有**WHERE**子句,用於指定行中每個綁定列的緩存值。 當它執行定位的更新語句時,游標庫會從行集緩衝區中的值更新其緩存。  
  
 有關 ODBC 游標庫的詳細資訊,請參閱本附錄的以下部分:  
  
-   [使用 ODBC 資料指標程式庫](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [執行定位的 Update 和 Delete 陳述式](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [資料指標程式庫程式碼範例](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [實施說明](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC 資料指標程式庫錯誤碼](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
