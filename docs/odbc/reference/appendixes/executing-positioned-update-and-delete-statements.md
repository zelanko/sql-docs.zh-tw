---
title: 執行定位的 Update 和 Delete 語句 |Microsoft Docs
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
ms.openlocfilehash: 2c69f784c2ce7c29cb49c81bf23f34a9cad12089
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67913624"
---
# <a name="executing-positioned-update-and-delete-statements"></a>執行定點更新和刪除陳述式
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 在應用程式使用**SQLFetchScroll**提取資料區塊之後，它就可以更新或刪除區塊中的資料。 若要執行定位的更新或刪除，應用程式：  
  
1.  呼叫**SQLSetPos** ，將資料指標置於要更新或刪除的資料列上。  
  
2.  使用下列語法來構造定位的 update 或 delete 語句：  
  
     **更新***資料表-名稱*  
  
     **設定**資料*行識別碼* **=** {*expression* &#124; **Null**}  
  
     [**，** 資料*行識別碼* **=** {*expression* &#124; **Null**}]  
  
     **其中目前的**資料*指標名稱*  
  
     **從***資料表名稱*中刪除**目前的**資料*指標名稱*  
  
     在定位 update 語句中建立**SET**子句最簡單的方式，是使用每個要更新之資料行的參數標記，並使用**SQLBindParameter**將這些資料系結至資料列集緩衝區，以便更新資料列。 在此情況下，參數的 C 資料型別將與資料列集緩衝區的 C 資料型別相同。  
  
3.  如果要執行定位的 update 語句，則更新目前資料列的資料列集緩衝區。 成功執行定位的 update 語句之後，資料指標程式庫會將目前資料列中每個資料行的值複製到其快取。  
  
    > [!CAUTION]  
    >  如果應用程式在執行定位的 update 語句之前未正確更新資料列集緩衝區，則在執行語句之後，快取中的資料將會不正確。  
  
4.  使用與資料指標相關聯的語句，執行定位的 update 或 delete 語句。  
  
    > [!CAUTION]  
    >  用來識別目前資料列的資料指標程式庫所建立的**WHERE**子句，可能無法識別任何資料列、識別不同的資料列，或識別一個以上的資料列。 如需詳細資訊，請參閱[建立搜尋的語句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 所有定位的 update 和 delete 語句都需要資料指標名稱。 若要指定資料指標名稱，應用程式會在開啟資料指標之前呼叫**SQLSetCursorName** 。 若要使用驅動程式所產生的資料指標名稱，應用程式會在開啟資料指標之後呼叫**SQLGetCursorName** 。  
  
 在資料指標程式庫執行定位的 update 或 delete 語句之後，資料指標程式庫所維護的狀態陣列、資料列集緩衝區和快取，會包含下表中顯示的值。  
  
|使用的語句|資料列狀態陣列中的值|中的值<br /><br /> 資料列集緩衝區|中的值<br /><br /> 快取緩衝區|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|定點更新|SQL_ROW_UPDATED|新值 [1]|新值 [1]|  
|已定位刪除|SQL_ROW_DELETED|舊值|舊值|  
  
 [1] 應用程式必須在執行定位的 update 語句之前，更新資料列集緩衝區中的值;在執行定位的 update 語句之後，游標程式庫會將資料列集緩衝區中的值複製到其快取。
