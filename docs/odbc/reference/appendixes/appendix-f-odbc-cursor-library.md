---
title: '附錄 f: ODBC 資料指標程式庫 |Microsoft 文件'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10e43272c7d9a75956aa162398c2869c558cdea1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="appendix-f-odbc-cursor-library"></a>附錄 f: ODBC 資料指標程式庫
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 ODBC 資料指標程式庫 (Odbccr32.dll) 的符合層級 1 API 的一致性層級的任何驅動程式支援區塊可捲動資料指標和可轉散發其應用程式或驅動程式的開發人員。 資料指標程式庫也支援定位的 update 和 delete 陳述式所產生之結果集**選取**陳述式。 雖然它支援只有靜態和順向資料指標時，資料指標程式庫可滿足許多應用程式的需求。 此外，它可以提供良好的效能，特別是小型至中型的結果集，以及沒有良好的資料指標支援的應用程式。  
  
 資料指標程式庫是位於驅動程式管理員與驅動程式之間的動態連結程式庫 (DLL)。 當應用程式呼叫函式時，驅動程式管理員會呼叫函式中的資料指標程式庫，可執行的函式，或者指定的驅動程式中呼叫它。 針對指定的連接，應用程式會指定資料指標程式庫會一律使用、 驅動程式不支援可捲動資料指標，如果使用或從未使用過。  
  
 資料指標程式庫會顯示為驅動程式管理員的驅動程式。 如果資料指標程式庫位於驅動程式管理員和 ODBC 2 之間。*x*驅動程式，資料指標程式庫會顯示為 ODBC 2。*x*驅動程式。 如果資料指標程式庫位於驅動程式管理員和 ODBC 3 之間 *.x*驅動程式，資料指標程式庫會顯示為 ODBC 3 *.x*驅動程式。 資料指標程式庫所展現的行為取決於驅動程式，使用繫結的位移，除了這兩個 ODBC 2 支援的版本。*x*和 ODBC 3。*x*驅動程式。  
  
 若要實作中的區塊資料指標**SQLFetch**和**SQLFetchScroll**，資料指標程式庫重複呼叫**SQLFetch**驅動程式中。 若要實作捲動，它會快取在記憶體和磁碟檔案中擷取的資料。 當應用程式要求新的資料列集時，資料指標程式庫會擷取它在必要時從驅動程式或快取。  
  
 若要實作定點的 update 和 delete 陳述式，資料指標程式庫建構**更新**或**刪除**陳述式搭配**其中**子句，指定的快取每個資料列中的繫結資料行的值。 當它執行的定位的 update 陳述式時，資料指標程式庫會更新其快取的資料列集的緩衝區中的值。  
  
 如需 ODBC 資料指標程式庫的詳細資訊，請參閱本附錄的下列各節：  
  
-   [使用 ODBC 資料指標程式庫](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [執行定位的 Update 和 Delete 陳述式](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [資料指標程式庫程式碼範例](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [實作注意事項](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC 資料指標程式庫錯誤碼](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
