---
title: 區塊資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc62e7b5225c434bac33630f2f0cf8f39c72bfc9
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52504681"
---
# <a name="block-cursors"></a>區塊資料指標
許多應用程式花費大量時間將在網路上的資料。 此時間部分所花費的實際透過網路將資料以及其中的組件所花費網路額外負荷，例如驅動程式發出要求的資料列呼叫。 可以降低後者的時間，如果應用程式會有效率地使用*區塊中，* 或是*fat* *資料指標，* 這可以一次傳回多個資料列。  
  
 應用程式永遠可以選擇使用區塊資料指標。 可以從中擷取一次只有一個資料列的資料來源，則必須模擬驅動程式中的區塊資料指標。 這可以由執行多個單一資料列擷取。 雖然這是不太可能提供任何效能提升，這會開啟應用程式的機會。 原生 Dbms 實作的區塊資料指標以及與這些 Dbms 相關聯的驅動程式將它們公開 （expose），這類應用程式則會發生的效能提升。  
  
 傳回單一擷取使用區塊資料指標中的資料列稱為*資料列集*。 請務必不要將混淆的結果集資料列集。 資料列集在應用程式緩衝區所維護時，就會在資料來源，維護的結果集。 雖然結果集固定的資料列集不是-它變更位置，並每次擷取一組新的資料列的內容。 就如同等傳統 SQL 順向資料指標指向目前的資料列的單一資料列資料指標，區塊資料指標會指向資料列集，可以視為*目前的資料列*。  
  
 已經提取的多個資料列的單一資料列執行作業的作業，應用程式必須先指定哪一個資料列是目前的資料列。 目前的資料列，才呼叫**SQLGetData**和定位 update 和 delete 陳述式。 區塊資料指標第一次傳回一個資料列集時，目前的資料列時，資料列集的第一個資料列。 若要變更目前的資料列，應用程式會呼叫**SQLSetPos**或是**SQLBulkOperations** （來依書籤更新）。 下圖顯示結果集、 資料列集、 目前資料列、 資料列集資料指標和區塊資料指標的關聯的性。 如需詳細資訊，請參閱[使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)在本節中，稍後並[定位更新和刪除陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)並[SQLSetPos 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
 ![接下來，擷取前，第一個和最後一個資料列集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 資料指標是否為區塊資料指標無關是否可捲動的內容。 比方說，大部分的報表應用程式中的工作是花在擷取和列印的資料列。 因為這個緣故，它會使用最快速的順向、 區塊資料指標。 它會使用順向資料指標來避免可捲動的資料指標和區塊資料指標，以減少網路流量的費用。  
  
 此章節包含下列主題。  
  
-   [繫結資料行以搭配使用區塊資料指標](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [資料列狀態陣列](../../../odbc/reference/develop-app/row-status-array.md)
