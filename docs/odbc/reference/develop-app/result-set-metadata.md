---
title: 結果集中繼資料 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ed379bf246bb25e60865092be5a0526fddc2aef0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="result-set-metadata"></a>結果集中繼資料
*中繼資料*是描述其他資料的資料。 例如，結果集中繼資料描述結果集，例如在結果集中的資料行數目、 資料類型的這些資料行，其名稱、 有效位數、 null 屬性，以及等等。  
  
 互通的應用程式應該永遠會檢查結果集資料行的中繼資料。 目錄函數所傳回之結果集中的資料行的中繼資料可能會不同資料行的中繼資料。 例如，假設 「 可更新的資料行包含在聯結兩個資料表建立結果集。 雖然**SQLColumnPrivileges**可能表示使用者可以更新資料行，請在結果集中繼資料可能不如果資料行聯結的 「 多 」 端上; 許多資料來源可以更新的聯結，但不是能在 「 一 」 端的資料行 」多 」 端。 甚至是資料類型不能假設為相同，因為資料來源可能會建立結果集時升級的資料類型。  
  
 此章節包含下列主題。  
  
-   [中繼資料的使用方式為何？](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
