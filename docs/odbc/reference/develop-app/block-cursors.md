---
title: "區塊資料指標 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7747f421fe4a7356086cf27ecf62739f34acdd17
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="block-cursors"></a>區塊資料指標
許多應用程式花費大量時間將資料匯聚在網路上。 此時間部分所花費的實際將資料匯聚透過網路，以及它的組件所花費網路額外負荷，例如驅動程式對要求的資料列的呼叫。 如果應用程式會有效率地使用，就可以降低後者的時間*區塊，*或*fat、* *資料指標，*可以一次傳回多個資料列。  
  
 應用程式永遠會有使用區塊資料指標的選項。 可從中擷取一次只有一個資料列的資料來源，必須在驅動程式模擬區塊資料指標。 執行多個單一資料列提取可以完成此動作。 雖然這是不太可能提供任何效能提升，它會開啟應用程式的機會。 Dbms 原生實作區塊資料指標以及與這些 Dbms 相關聯的驅動程式將它們公開，這類應用程式再將經歷的效能提升。  
  
 傳回單一使用區塊資料指標提取的資料列稱為*資料列集*。 務必不混淆的結果集資料列集。 維護應用程式緩衝區資料列集時，就會在資料來源，維護結果集。 資料列集結果集固定的而不是，它變更位置，並每次擷取一組新的資料列的內容。 例如傳統 SQL 順向資料指標指向的目前資料列的單一資料列資料指標，如同一般區塊資料指標會指向資料列集，可以視為*目前資料列*。  
  
 已經提取的多個資料列時，請在單一資料列上執行作業，應用程式必須先指定哪一個資料列是目前的資料列。 目前的資料列所需的呼叫**SQLGetData**和定位 update 和 delete 陳述式。 當區塊資料指標第一次傳回一個資料列集時，目前的資料列是資料列集的第一個資料列。 若要變更目前的資料列，應用程式會呼叫**SQLSetPos**或**SQLBulkOperations** （若要更新書籤）。 下圖顯示結果集、 資料列集、 目前資料列、 資料列集資料指標和區塊資料指標的關聯的性。 如需詳細資訊，請參閱[使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)稍後在本章節，和[定位的更新和刪除陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)和[更新的資料與 SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
 ![接下來，擷取前，第一個和最後一個資料列集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 資料指標是否為區塊資料指標無關是否可捲動。 例如，大部分的報表應用程式中的工作是花在擷取及列印的資料列。 因為這個緣故，它會使用最快速順向、 區塊資料指標。 它使用順向資料指標來避免可捲動資料指標和區塊資料指標，以減少網路流量的費用。  
  
 此章節包含下列主題。  
  
-   [繫結區塊資料指標搭配使用的資料行](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [資料列狀態陣列](../../../odbc/reference/develop-app/row-status-array.md)

