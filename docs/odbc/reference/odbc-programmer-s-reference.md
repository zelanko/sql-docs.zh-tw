---
description: ODBC 程式設計人員&#39;s 參考
title: ODBC 程式設計人員&#39;s 參考 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09d79d9a71b1eaeadf6fd649e7433cf5133de403
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428990"
---
# <a name="odbc-programmer39s-reference"></a>ODBC 程式設計人員&#39;s 參考
ODBC 程式設計 *人員參考* 包含下列各節。  
  
-   [ODBC 3.8 的新](../../odbc/reference/what-s-new-in-odbc-3-8.md) 功能列出 Windows 8 SDK 中新增的 odbc 功能。  
  
-   [範例 Odbc 程式](../../odbc/reference/sample-odbc-program.md) 展示了 odbc 程式範例。  
  
-   [Odbc 簡介](../../odbc/reference/introduction-to-odbc.md) 提供了結構化查詢語言 (SQL) 和 odbc 的簡短歷程記錄，以及有關 odbc 介面的概念資訊。  
  
-   [開發應用程式](../../odbc/reference/develop-app/developing-applications.md) 包含開發應用程式的相關資訊，這些應用程式使用 ODBC 介面和執行它的驅動程式。  
  
-   [安裝及設定 ODBC 軟體](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) 會提供安裝和安裝 DLL 函式參考的相關資訊。  
  
-   [開發 ODBC 驅動程式](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) 包含關於撰寫驅動程式的資訊。  
  
-   [API 參考](../../odbc/reference/syntax/odbc-reference.md) 包含所有 ODBC 函數的語法和語義資訊。  
  
-   [Odbc 附錄](../../odbc/reference/appendixes/odbc-appendixes.md) 包含 odbc 錯誤碼、資料類型和 SQL 文法的技術詳細資料和參考資料表。  
  
## <a name="working-with-the-odbc-documentation"></a>使用 ODBC 檔  
 ODBC 介面是專為搭配 C 程式設計語言使用所設計。 ODBC 介面可用於下列三方面︰SQL 陳述式、ODBC 函式呼叫和 C 程式設計。 本檔假設下列各項：  
  
-   使用 C 程式設計語言的知識。  
  
-   一般 DBMS 知識並熟悉 SQL。  
  
 使用下列印刷樣式慣例。  
  
|格式|用於|  
|------------|--------------|  
|SELECT * FROM|大寫字母指出作業系統命令層級所使用的 SQL 語句、宏名稱和詞彙。|  
|`RETCODE SQLFetch(hdbc)`|等寬字型用於範例命令列和程式碼。|  
|*引數*|斜體單字表示以程式設計的方式引數、使用者或應用程式必須提供的資訊，或是文字強調。|  
|**SQLEndTran**|粗體類型表示語法的輸入必須與顯示的完全相同，包括函數名稱。|  
|&#124;|分隔號會在語法行中分隔兩個互斥的選項。|  
|...|省略號表示引數可以重複數次。|  
|. . .|三個點的資料行表示接續先前的程式程式碼。|  
  
## <a name="about-the-code-examples"></a>關於程式碼範例  
 本指南中的程式碼範例僅供說明之用。 因為它們主要是為了示範 ODBC 原則而撰寫，所以在清楚起見的情況下，有時候會有更高的效率。 此外，為了清楚起見，有時會省略程式碼的整個區段。 其中包括非 ODBC 函式的定義 (這些函式的名稱不能以 "SQL" 開頭 ) 和大部分的錯誤處理。  
  
 所有程式碼範例都使用 ANSI 字串和相同的資料庫架構，這會顯示在 [目錄](../../odbc/reference/develop-app/catalog-functions.md)函式的開頭。  
  
## <a name="recommended-reading"></a>建議閱讀資料  
 如需 SQL 的詳細資訊，請使用下列標準：  
  
-   具有完整性增強功能的資料庫語言-SQL、ANSI、1989 ANSI X 3.135-1989 年。  
  
-   資料庫語言-SQL： ANSI X3H2 和 ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92) 。  
  
-   Open Group，資料管理：結構化查詢語言 (SQL)  (SQL) ，第2版 (開啟的群組 1996) 。  
  
 除了標準和廠商專屬的 SQL 指南之外，許多書籍也會說明 SQL，包括：  
  
-   Date、c.、with Darwen、Hugh： *SQL Standard* (Addison-Wesley、1993) 指南。  
  
-   Emerson、Sandra L.、Darnovsky、Marcy 和 Bowman，Judith S.： *實際的 SQL 手冊* (Addison-Wesley，1989) 。  
  
-   Groff、James R 和 Weinberg，Paul N.： *使用 SQL* (Osborne Mcgraw-hill-峰，1990) 。  
  
-   Gruber，聖馬丁： *瞭解 SQL* (Sybex，1990) 。  
  
-   Hursch、、Carolyn J.： *SQL、結構化查詢語言 (SQL) * (索引標籤手冊、1988) 。  
  
-   Melton、Jim 和 Simon，Alan R.： *瞭解新的 SQL：完整的指南* (Morgan Kaufmann 發行者，1993) 。  
  
-   Pascal、Fabian： *SQL 和關聯式基本概念* (M & 的書籍，1990) 。  
  
-   Trimble、Harvey、Jr 和 Chappell，David： SQL (Wiley *的視覺化簡介* ，1989) 。  
  
-   Van der Lan，Rick F.： *SQL* (Addison 簡介-Wesley，1988) 。  
  
-   Vang、Soren： *SQL 和關係資料庫* (Microtrend 書籍，1990) 。  
  
-   Viescas，John： SQL (Microsoft Corp. 1989) 的 *快速參考指南* 。  
  
 如需交易處理的詳細資訊，請參閱：  
  
-   灰色、J. N。 和 Reuter，Andreas： *交易處理：概念和技巧* (Morgan Kaufmann 發行者，1993) 。  
  
-   Hackathorn，Richard d.： *Enterprise Database Connectivity* (Wiley & 兒子，1993) 。  
  
 如需呼叫層級介面的詳細資訊，請使用下列標準：  
  
-   開啟群組、 *資料管理： SQL 呼叫層級介面 (CLI) 、C451* (開啟群組、1995) 。  
  
-   ISO/IEC 9075-3:1995、呼叫層級介面 (SQL/CLI) 。  
  
 如需 ODBC 的詳細資訊，有許多書籍可供使用，包括：  
  
-   Geiger、Kyle： *在 ODBC (中* ，Microsoft 請按® 1995) 。  
  
-   Gryphon、Robert、Charpentier、L u c、Oelschlager、Jon、Shoemaker、Andrew、Cross、Jim 和 Lilley、Albert W.： *使用 ODBC 2* (Que，1994) 。  
  
-   約翰約翰、Tom 和 Osborne、Mark： *ODBC 開發人員指南* (Howard & 公司，1994) 。  
  
-   北美洲，Ken： *Windows 多 DBMS 程式設計：使用 c + +、Visual Basic、ODBC、OLE 2 和 Tools FOR DBMS 專案* (John Wiley & 兒子，inc.，1995) 。  
  
-   Stegman、Michael O.、Signore、Robert 和 Creamer、John： *ODBC 解決方案、分散式環境中的開放式資料庫連接* (Mcgraw-hill-峰、1995) 。  
  
-   Welch，Keith： *使用 ODBC 2* (Que，1994) 。  
  
-   Whiting，帳單： *在二十天內教授 ODBC* (Howard & 公司，1994) 。
