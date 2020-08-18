---
description: 附錄 F：ODBC 資料指標程式庫
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 325c7cdc5d2fb185ef3dbd2500a20230d90193bf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411424"
---
# <a name="appendix-f-odbc-cursor-library"></a>附錄 F：ODBC 資料指標程式庫
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 ODBC 資料指標程式庫 ( # A0) 支援針對符合層級 1 API 一致性層級的任何驅動程式封鎖可滾動的資料指標，並可讓開發人員使用其應用程式或驅動程式轉散發。 資料指標程式庫也支援 **SELECT** 語句所產生之結果集的定點更新和刪除語句。 雖然它僅支援靜態和順向資料指標，但資料指標程式庫符合許多應用程式的需求。 此外，它可以提供良好的效能，特別是針對小型到中型的結果集，以及沒有良好資料指標支援的應用程式。  
  
 資料指標程式庫是位於驅動程式管理員和驅動程式之間 (DLL) 的動態連結程式庫。 當應用程式呼叫函式時，驅動程式管理員會呼叫資料指標程式庫中的函式，該函式會執行函數或在指定的驅動程式中呼叫它。 針對指定的連接，應用程式會指定是否一律使用資料指標程式庫，如果驅動程式不支援可滾動的資料指標，則會使用，或從未使用。  
  
 資料指標程式庫會顯示為驅動程式管理員的驅動程式。 如果資料指標程式庫位於驅動程式管理員和 ODBC 2.x 驅動程式之間，則資料指標程式庫會顯示為*ODBC 2.x* *驅動程式。* 如果資料指標程式庫位於驅動程式管理員和 ODBC 3.x 驅動程式之間，則資料指標程式庫會顯示為*ODBC 3.x* *驅動程式。* 資料指標程式庫所呈現的行為取決於它所使用的驅動程式版本，除了系結位移之外，ODBC *2.x 和 odbc* *3.x 驅動程式* 都支援此功能。  
  
 若要在 **SQLFetch** 和 **SQLFetchScroll**中執行區塊資料指標，資料指標程式庫會重複呼叫驅動程式中的 **SQLFetch** 。 為了進行滾動，它會快取在記憶體和磁片檔案中取出的資料。 當應用程式要求新的資料列集時，資料指標程式庫會視需要從驅動程式或快取進行抓取。  
  
 若要執行定位的 update 和 delete 語句，資料指標程式庫會使用**WHERE**子句來建立**update**或**delete**語句，以指定資料列中每個系結資料行的快取值。 當它執行定位的 update 語句時，資料指標程式庫會從資料列集緩衝區中的值更新其快取。  
  
 如需 ODBC 資料指標程式庫的詳細資訊，請參閱此附錄的下列章節：  
  
-   [使用 ODBC 資料指標程式庫](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [執行定位的 Update 和 Delete 陳述式](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [資料指標程式庫程式碼範例](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [實作附註](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC 資料指標程式庫錯誤碼](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
