---
title: "執行 Update 和 Delete 陳述式置於 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 78bdb77c8aa4d9351e040b97d9690bb09374856d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="executing-positioned-update-and-delete-statements"></a>執行定位的 Update 和 Delete 陳述式
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 應用程式提取的資料區塊之後**SQLFetchScroll**、 更新或刪除在區塊中的資料。 若要執行定位的更新或刪除，應用程式：  
  
1.  呼叫**SQLSetPos**以將游標放在要更新或刪除的資料列。  
  
2.  建構的定位的更新或刪除陳述式搭配下列語法：  
  
     **更新***資料表名稱*  
  
     **設定***資料行識別碼*  **=**  {*運算式*&#124;**NULL**}  
  
     [**，** *資料行識別碼*  **=**  {*運算式*&#124;**NULL**}]  
  
     **WHERE CURRENT OF** *資料指標名稱*  
  
     **DELETE FROM** *資料表名稱* **WHERE CURRENT OF** *資料指標名稱*  
  
     最簡單的方式來建構**設定**定位的 update 陳述式中的子句是使用參數標記，每個資料行更新，並使用**SQLBindParameter**繫結至資料列集的緩衝區若要更新的資料列。 在此情況下，參數的 C 資料類型會與資料列集緩衝區的 C 資料類型相同。  
  
3.  如果將執行的定位的 update 陳述式會更新目前的資料列的資料列集的緩衝區。 已成功在執行之後的定位的 update 陳述式，資料指標程式庫會複製目前的資料列中的每個資料行至其快取值。  
  
    > [!CAUTION]  
    >  如果應用程式不會正確地更新資料列集緩衝區，以執行定位的 update 陳述式之前，執行陳述式之後，會不正確快取中的資料。  
  
4.  執行定位的更新或 delete 陳述式使用不同的陳述式與資料指標相關聯的陳述式。  
  
    > [!CAUTION]  
    >  **其中**子句所識別的目前資料列的資料指標程式庫建構無法識別任何資料列、 識別不同的資料列，或識別一個以上的資料列。 如需詳細資訊，請參閱[建構搜尋陳述式](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 所有定位 update 和 delete 陳述式需要資料指標名稱。 若要指定資料指標名稱，應用程式呼叫**SQLSetCursorName**資料指標開啟之前。 若要使用驅動程式所產生的資料指標名稱，應用程式呼叫**SQLGetCursorName**資料指標開啟後。  
  
 游標後的程式庫執行定位的更新或刪除陳述式、 狀態陣列、 資料列集緩衝區和維護的資料指標程式庫的快取包含下表中所顯示的值。  
  
|使用陳述式|資料列狀態陣列中的值|中的值<br /><br /> 資料列集的緩衝區|中的值<br /><br /> 快取緩衝區|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|定點更新|SQL_ROW_UPDATED|新的值 [1]|新的值 [1]|  
|定位的 delete|SQL_ROW_DELETED|舊的值|舊的值|  
  
 [1] 的應用程式必須執行定位的 update 陳述式; 之前更新的資料列集的緩衝區中的值在執行之後定位的 update 陳述式，資料指標程式庫會複製值到快取資料列集緩衝區中。

