---
title: 結構描述檢視 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema views [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], schema views
ms.assetid: f1dfb3e8-a7bd-46c3-92b6-c19531e8409d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 782dec08b76a9e5a97719d6af39e2c30c0f92d19
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468615"
---
# <a name="schema-views"></a>結構描述檢視
應用程式在呼叫 ODBC 目錄函數，或使用 INFORMATION_SCHEMA 檢視，可以從 DBMS 擷取中繼資料資訊。 ANSI SQL-92 標準所定義的檢視。  
  
 如果 DBMS 和驅動程式支援，INFORMATION_SCHEMA 檢視會提供更強大且最完整的方法，擷取中繼資料，比 ODBC 目錄函數所提供。 應用程式可以執行自己的自訂**選取**陳述式是否符合其中一個檢視，可以加入檢視，或可以在檢視上執行聯集。 同時提供更高的公用程式與更廣泛的中繼資料，INFORMATION_SCHEMA 檢視不常受到 DBMS。 這可能會變更為更多的 Dbms 和驅動程式達成與 SQL-92 的相容性。  
  
 若要判斷支援哪些檢視，應用程式會呼叫**SQLGetInfo** SQL_INFO_SCHEMA_VIEWS 選項。 若要從支援的檢視中擷取中繼資料，應用程式執行**選取**陳述式，指定所需的結構描述資訊。
