---
title: 附錄 F： ODBC 資料指標程式庫 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bfffd95dd88b0a25be682a3df581e55825ed9ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68090827"
---
# <a name="appendix-f-odbc-cursor-library"></a>附錄 F：ODBC 資料指標程式庫
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 ODBC 資料指標程式庫（Odbccr32）支援針對符合層級 1 API 一致性層級的任何驅動程式封鎖可滾動游標，並可供開發人員與其應用程式或驅動程式轉散發。 資料指標程式庫也支援**SELECT**語句所產生之結果集的定位 update 和 delete 語句。 雖然它僅支援靜態和順向資料指標，但資料指標程式庫可滿足許多應用程式的需求。 此外，它可以提供良好的效能，特別是針對小型到中型的結果集，以及沒有良好資料指標支援的應用程式。  
  
 游標程式庫是位於驅動程式管理員和驅動程式之間的動態連結程式庫（DLL）。 當應用程式呼叫函數時，驅動程式管理員會呼叫資料指標程式庫中的函式，而該函式會執行函式，或在指定的驅動程式中呼叫該函數。 針對指定的連接，應用程式會指定是否一律使用資料指標程式庫，如果驅動程式不支援可滾動的資料指標，或從未使用過它，則使用它。  
  
 資料指標程式庫會顯示為驅動程式管理員的驅動程式。 如果資料指標程式庫位於驅動程式管理員和 ODBC 2.x 驅動程式之間，則資料指標程式庫會顯示為*odbc 2.x* *驅動程式。* 如果資料指標程式庫位於驅動程式管理員和 ODBC 3.x 驅動程式之間，則資料指標程式庫會顯示為*odbc 3.x* *驅動程式。* 資料指標程式庫所呈現的行為取決於其所使用的驅動程式版本，但系結位移除外，這同時支援 ODBC *2.x 和 odbc* *3.x 驅動程式*。  
  
 若要在**SQLFetch**和**SQLFetchScroll**中執行區塊資料指標，游標程式庫會重複呼叫驅動程式中的**SQLFetch** 。 為了執行滾動，它會快取在記憶體中和磁片檔案中抓取的資料。 當應用程式要求新的資料列集時，資料指標程式庫會視需要從驅動程式或快取中抓取。  
  
 若要執行定位的 update 和 delete 語句，資料指標程式庫會使用**WHERE**子句來建立**update**或**delete**語句，以指定資料列中每個系結資料行的快取值。 當它執行定位的 update 語句時，資料指標程式庫會從資料列集緩衝區中的值更新其快取。  
  
 如需有關 ODBC 資料指標程式庫的詳細資訊，請參閱本附錄的下列各節：  
  
-   [使用 ODBC 資料指標程式庫](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [執行定點更新和刪除陳述式](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [資料指標程式庫程式碼範例](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [實作附註](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC 資料指標程式庫錯誤碼](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
