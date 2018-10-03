---
title: 執行定位的 Update 和 Delete 陳述式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2391c01d93c876562ab9d870ab0dba22bf74cea5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772046"
---
# <a name="executing-positioned-update-and-delete-statements"></a>執行定點更新和刪除陳述式
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 應用程式提取的資料區塊之後**SQLFetchScroll**，它可以更新或刪除在區塊中的資料。 若要執行定位的 update 或 delete，應用程式：  
  
1.  呼叫**SQLSetPos**若要將游標放在要更新或刪除的資料列。  
  
2.  建構定位的 update 或 delete 陳述式，使用下列語法：  
  
     **更新***資料表名稱*  
  
     **設定***資料行識別碼* **=** {*運算式* &#124; **NULL**}  
  
     [**，** *資料行識別碼* **=** {*運算式* &#124; **NULL**}]  
  
     **WHERE CURRENT OF** *資料指標名稱*  
  
     **DELETE FROM** *資料表名稱* **WHERE CURRENT OF** *資料指標名稱*  
  
     最簡單的方式來建構**設定**定位的 update 陳述式中的子句是使用每個資料行的參數標記更新，並使用**SQLBindParameter**繫結到資料列集的緩衝區要更新的資料列。 在此情況下，參數的 C 資料類型會與資料列集緩衝區的 C 資料類型相同。  
  
3.  如果它將會執行定位的 update 陳述式會更新目前的資料列的資料列集的緩衝區。 已成功執行之後的定位的 update 陳述式，資料指標程式庫會複製值，從目前的資料列中的每個資料行至其快取。  
  
    > [!CAUTION]  
    >  如果應用程式不會正確更新的資料列集的緩衝區，以執行定位的 update 陳述式之前，快取中的資料會不正確之後執行的陳述式。  
  
4.  執行定位的 update 或 delete 陳述式使用不同的陳述式，比資料指標相關聯的陳述式。  
  
    > [!CAUTION]  
    >  **其中**建構的資料指標程式庫，以識別目前的資料列的子句無法識別的任何資料列、 找出不同的資料列，或識別一個以上的資料列。 如需詳細資訊，請參閱 <<c0> [ 建構搜尋的陳述式](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 所有定位 update 和 delete 陳述式需要資料指標名稱。 若要指定資料指標名稱，應用程式會呼叫**SQLSetCursorName**資料指標開啟之前。 若要使用驅動程式所產生的資料指標名稱，應用程式會呼叫**SQLGetCursorName**資料指標開啟後。  
  
 之後資料指標程式庫執行定位的 update 或 delete 陳述式、 狀態陣列、 資料列集的緩衝區，以及資料指標程式庫所維護的快取包含下表中顯示的值。  
  
|使用陳述式|資料列狀態陣列中的值|中的值<br /><br /> 資料列集的緩衝區|中的值<br /><br /> 快取緩衝區|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|定點更新|SQL_ROW_UPDATED|新的值 [1]|新的值 [1]|  
|定位的 delete|SQL_ROW_DELETED|舊值|舊值|  
  
 [1] 的應用程式必須執行定位的 update 陳述式中; 之前更新的資料列集的緩衝區中的值執行定位的 update 陳述式之後，資料指標程式庫會複製值至其快取中的資料列集的緩衝區。
