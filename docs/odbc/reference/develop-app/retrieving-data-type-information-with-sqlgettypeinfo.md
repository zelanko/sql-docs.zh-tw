---
title: 使用 SQLGetTypeInfo 檢索資料類型資訊 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ec2bbba824eaf3d74133cf9754eca2593c9fb79
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300058"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>使用 SQLGetTypeInfo 擷取資料類型資訊
由於從基礎 SQL 資料類型到 ODBC 類型識別碼的映射是近似的,因此 ODBC 提供了函數 (**SQLGetTypeInfo),** 驅動程式可以透過該函數完全描述資料來源中的每個 SQL 資料類型。 此函數返回一個結果集,其中每行描述單個數據類型的特徵,如名稱、類型標識符、精度、縮放和null。  
  
 通常,允許使用者創建和更改表的通用應用程式可以使用此資訊。 此類應用程式呼叫**SQLGetTypeInfo**來檢索資料類型資訊,然後將部分或全部資訊呈現給使用者。 此類應用程式需要瞭解兩件事:  
  
-   多個 SQL 資料類型可以映射到單個類型識別碼,這會使很難確定要使用的數據類型。 為了解決這個問題,結果集首先按類型標識符排序,第二個按與類型標識符定義的接近排序。 此外,數據源定義的數據類型優先於使用者定義的數據類型。 例如,假設數據源將 INTEGER 和 COUNTER 數據類型定義為相同,但 COUNTER 是自動遞增的。 還假設使用者定義的類型"WHOLENUM"是 INTEGER 的同義詞。 每種類型都映射到SQL_INTEGER。 在**SQLGetTypeInfo**結果集中,INTEGER 首先出現,然後是「反」, 然後是「反」。。 在 INTEGER 之後出現,因為它是使用者定義的,但在 COUNTER 之前,因為它更符合SQL_INTEGER類型標識符的定義。  
  
-   ODBC 不定義資料類型名稱,用於**創建表**和**ALTER TABLE**語句。 相反,應用程式應使用**SQLGetTypeInfo**返回的結果集的TYPE_NAME列中返回的名稱。 原因是,儘管大多數 SQL 在 DBMS 之間變化不大,但數據類型名稱差異很大。 ODBC 要求應用程式首先使用特定於 DBMS 的名稱,而不是強制驅動程式解析 SQL 語句並將標準數據類型名稱替換為特定於 DBMS 的數據類型名稱。  
  
 請注意 **,SQLGetTypeInfo**不一定描述應用程式可能遇到的所有數據類型。 特別是,結果集可能包含數據源不支持的數據類型。 例如,目錄函數返回的結果集中的列的數據類型由 ODBC 定義,數據源可能不支援這些數據類型。 要確定結果集中資料類型的特徵,應用程式呼叫**SQLColAttribute**。
