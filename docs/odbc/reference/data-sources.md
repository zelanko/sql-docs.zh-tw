---
title: 資料來源 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b7e464963471b0cad41c5b93d50507d0fa9bf96
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306509"
---
# <a name="data-sources"></a>資料來源
*數據源*只是數據源。 它可以是檔、DBMS 上的特定資料庫,甚至是即時數據饋送。 數據可能位於與程式相同的電腦上,或者位於網路上的另一台電腦上。 例如,資料源可能是運行在 OS/2® 作業系統上的 Oracle DBMS,由 Novell® Netware 訪問;通過閘道存取的 IBM DB2 DBMS;伺服器目錄中的 Xbase 檔的集合;或本地 Microsoft®訪問資料庫檔。  
  
 數據來源的目的是將資料(驅動程式名稱、網路位址、網路軟體等)收集到單個位置,並將其隱藏到單個位置,並將其隱藏到使用者位置。 用戶應該能夠查看包含工資單、庫存和人員的清單,從清單中選擇"工資單",讓應用程式連接到工資單數據,而不知道工資數據駐留的位置或應用程式如何訪問它。  
  
 術語*數據源*不應與類似的術語混淆。 在本手冊中 *,DBMS*或*資料庫*是指資料庫程式或引擎。 *桌面資料庫*(設計為在個人電腦上運行且通常缺乏完整的 SQL 和事務支援)和*伺服器資料庫*(旨在在用戶端/伺服器情況下運行,其特點是獨立資料庫引擎和豐富的 SQL 和事務支援)之間進一步進行了區分。 *資料庫*還引用特定的數據集合,例如目錄中的 Xbase 檔集合或 SQL Server 上的資料庫。 它通常等效於本手冊其他部分使用的術語*目錄*,或早期版本的 ODBC 中的字語*修飾詞*。  
  
 此章節包含下列主題。  
  
-   [資料來源的類型](../../odbc/reference/types-of-data-sources.md)  
  
-   [使用資料來源](../../odbc/reference/using-data-sources.md)  
  
-   [資料來源範例](../../odbc/reference/data-source-example.md)
