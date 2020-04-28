---
title: 結果集中繼資料 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300078"
---
# <a name="result-set-metadata"></a>結果集中繼資料
*元*資料是描述其他資料的資料。 例如，結果集中繼資料會描述結果集，例如結果集中的資料行數目、那些資料行的資料類型、其名稱、有效位數、null 屬性等等。  
  
 互通的應用程式應該一律檢查結果集資料行的中繼資料。 結果集中資料行的中繼資料，可能與目錄函數所傳回之資料行的中繼資料不同。 例如，假設可更新的資料行包含在聯結兩個數據表所建立的結果集中。 雖然**SQLColumnPrivileges**可能表示使用者可以更新資料行，但如果資料行位於聯結的「多」端，則結果集中繼資料可能不會出現;許多資料來源都可以更新聯結「一」端的資料行，而不是「多」端。 即使資料類型也無法假設為相同，因為資料來源可能會在建立結果集時升級資料類型。  
  
 此章節包含下列主題。  
  
-   [中繼資料的使用方式為何？](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
