---
title: 結果集元資料 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b78cdeb4c8b3522f4677c0277401cd9395a36a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300078"
---
# <a name="result-set-metadata"></a>結果集中繼資料
*元數據*是描述其他數據的數據。 例如,結果集元數據描述結果集,如結果集中的列數、這些列的數據類型、名稱、精度、空值等。  
  
 可互操作的應用程式應始終檢查結果集列的元數據。 結果集中列的元數據可能與目錄函數返回的列的元數據不同。 例如,假設一個可增加的列包含在通過聯接兩個表創建的結果集中。 雖然**SQLColumn 特權**可能指示使用者可以更新列,但如果列位於聯接的「多」側,則結果集元數據可能不會;許多數據源可以更新聯接的「一」端的列,但不能更新「多」端的列。 不能假定數據類型相同,因為數據源可能在創建結果集時提升數據類型。  
  
 此章節包含下列主題。  
  
-   [中繼資料的使用方式為何？](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
