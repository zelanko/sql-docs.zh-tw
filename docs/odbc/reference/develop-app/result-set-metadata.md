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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7dc88892fab2fd18dbcbec5ce54fa09c9c9b89e7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199386"
---
# <a name="result-set-metadata"></a>結果集中繼資料
*中繼資料*是描述其他資料的資料。 例如，結果集中繼資料會描述結果集，例如在結果集中的資料行數目、 這些資料行，其名稱、 有效位數、 null 屬性和等等的資料類型。  
  
 互通的應用程式應該永遠會檢查結果集資料行的中繼資料。 目錄函式所傳回的資料行的中繼資料可能會與不同結果集中的資料行的中繼資料。 例如，假設在聯結兩個資料表建立的結果集中包含的可更新的資料行。 雖然**SQLColumnPrivileges**可能表示使用者可以更新資料行，結果集中繼資料可能沒有資料行是否在聯結的 「 多 」 端上; 許多資料來源可以更新聯結的但不是能在 「 一 」 端的資料行 」多 」 端。 即使資料類型不能假設為相同，因為資料來源可能會同時建立結果集升級的資料類型。  
  
 此章節包含下列主題。  
  
-   [中繼資料的使用方式為何？](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
