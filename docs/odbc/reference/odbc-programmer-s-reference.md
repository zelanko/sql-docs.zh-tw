---
title: "ODBC 程式設計人員 &#39; s 參考 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b934652505039a021d2b08c0fa5314614ce9c609
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-programmer39s-reference"></a>ODBC 程式設計人員 &#39; s 參考
*ODBC 程式設計人員參考*包含下列各節。  
  
-   [What's New in ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md)列出 Windows 8 SDK 中所加入的新 ODBC 功能。  
  
-   [範例 ODBC 程式](../../odbc/reference/sample-odbc-program.md)呈現 ODBC 程式範例。  
  
-   [ODBC 簡介](../../odbc/reference/introduction-to-odbc.md)提供簡短的歷程記錄的結構化查詢語言和 ODBC，以及 ODBC 介面的概念性資訊。  
  
-   [開發應用程式](../../odbc/reference/develop-app/developing-applications.md)包含開發使用 ODBC 介面和實作該類別的驅動程式的應用程式的相關資訊。  
  
-   [安裝和設定 ODBC 軟體](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md)提供安裝和設定 DLL 函式參考的相關資訊。  
  
-   [ODBC 驅動程式的開發](../../odbc/reference/develop-driver/developing-an-odbc-driver.md)包含撰寫印表機驅動程式的相關資訊。  
  
-   [API 參考](../../odbc/reference/syntax/odbc-reference.md)包含語法與所有 ODBC 函數的語意資訊。  
  
-   [ODBC 附錄](../../odbc/reference/appendixes/odbc-appendixes.md)包含技術詳細資料與參考資料表的 ODBC 錯誤碼、 資料類型，以及 SQL 文法。  
  
## <a name="working-with-the-odbc-documentation"></a>使用 ODBC 文件  
 ODBC 介面可供使用的 C 程式設計語言使用。 使用 ODBC 介面跨越三個區域： SQL 陳述式，ODBC 函數呼叫和 C 程式設計。 這份文件會假設下列：  
  
-   使用 C 程式設計語言的知識。  
  
-   一般 DBMS 知識庫，並熟悉 SQL。  
  
 會使用下列的印刷慣例。  
  
|[格式]|用於|  
|------------|--------------|  
|選取 * 從|大寫字母表示 SQL 陳述式、 巨集名稱和作業系統命令層級使用的詞彙。|  
|`RETCODE SQLFetch(hdbc)`|等寬字型用於命令列範例和程式碼。|  
|*引數*|設為斜體的文字表示以程式設計方式的引數，資訊的使用者或應用程式必須提供的資料或文字的強調。|  
|**SQLEndTran**|粗體類型表示語法必須完全如下所示，包括函式名稱輸入。|  
|&#124;|分隔號會分隔語法列中的兩個互斥的選項。|  
|...|省略符號表示引數可以重複多次。|  
|執行個體時提供 SQL Server 登入。 執行個體時提供 SQL Server 登入。 執行個體時提供 SQL Server 登入。|三個點的資料行指出接續前一個程式碼的行。|  
  
## <a name="about-the-code-examples"></a>關於程式碼範例  
 本指南中的程式碼範例是僅供說明用途設計的。 已寫入主要是為了示範 ODBC 原則，因為效率有時已設定擱置在一旁為了清楚起見。 此外，程式碼的整個區段有時已省略為了清楚起見。 這些包括非 ODBC 函數 （名稱 [SQL] 不會啟動這些函式） 和大部分的錯誤處理的定義。  
  
 所有的程式碼範例會使用 ANSI 字串和相同的資料庫結構描述，其會顯示在開始[目錄函數](../../odbc/reference/develop-app/catalog-functions.md)。  
  
## <a name="recommended-reading"></a>建議閱讀資料  
 如需 SQL 的詳細資訊，下列標準可用：  
  
-   資料庫語言-SQL 搭配完整性增強功能，ANSI、 1989 ANSI X3.135 1989。  
  
-   資料庫語言-SQL: ANSI X3H2 和 ISO/IEC JTC1/SC21/WG3 9075:1992 (sql-92)。  
  
-   開啟 群組、 資料管理： 結構化的查詢語言 (SQL) 版本 2 (Open Group，1996年)。  
  
 除了標準與廠商特定 SQL 指南，許多書籍會描述 SQL，包括：  
  
-   日期、 C.J.，與 Darwen，Hugh: *SQL 標準的指南*(Addison-wesley，1993年)。  
  
-   就、 Sandra L、 Darnovsky、 Marcy 和 Bowman，Judith S:*實際 SQL 手冊*(Addison-wesley，1989年)。  
  
-   Groff，James R 和 Weinberg，Paul N:*使用 SQL* （Osborne McGraw-山勢阻擋，1990年）。  
  
-   Gruber Martin:*了解 SQL* (Sybex 1990)。  
  
-   Hursch 端子 l 和林麗 J.: *SQL、 結構化的查詢語言*（索引標籤的書籍，1988年）。  
  
-   Melton、 Jim 和 Simon，Alan R:*了解新的 SQL： 完整指南*（Morgan Kaufmann 發行者，1993年）。  
  
-   依照 pascal 命名法、 Fabian: *SQL 與關聯式的基本概念*(& T 書籍，1990年)。  
  
-   Trimble、 J.Harvey，與和 Chappell，David: *SQL Visual 簡介*(Wiley，1989)。  
  
-   Van der Lan、 Rick F.: *Introduction to SQL* (Addison-wesley，1988年)。  
  
-   Vang、 Soren: *SQL 和關聯式資料庫*（Microtrend 書籍，1990年）。  
  
-   Viescas，John: *to SQL 的快速參照指南*（Microsoft corp.著作權，1989年）。  
  
 如需有關交易處理的詳細資訊，請參閱：  
  
-   灰色顯示，J.n。 Reuter、 Andreas:*交易處理： 概念和技術*（Morgan Kaufmann 發行者，1993年）。  
  
-   Hackathorn Richard D:*企業資料庫連線*(Wiley （& c) 1993年，天)。  
  
 如需呼叫層級介面的詳細資訊，下列標準可用：  
  
-   Open Group*資料管理： SQL 呼叫層級介面 (CLI) (C451* (Open Group 1995)。  
  
-   ISO/IEC 9075-3:1995，呼叫層級介面 (SQL/CLI)。  
  
 如需有關 ODBC 中，有多個的書籍，包括：  
  
-   Geiger Kyle:*內 ODBC* (Microsoft Press® 1995)。  
  
-   Gryphon、 Robert、 Charpentier、 Luc、 Oelschlager Jon、 Shoemaker，Andrew 跨 Jim 和 Lilley、 希望工時：*使用 ODBC 2* （佇列，1994年）。  
  
-   標記 Johnston，Tom 和 Osborne，： *ODBC 開發人員手冊*(Howard 工時 Sam & 公司，1994年)。  
  
-   North，Ken: *Windows 多重 DBMS 程式設計： 為 DBMS 專案中使用 c + +、 Visual Basic、 ODBC、 OLE 2 和工具*(John Wiley & 天，Inc.，1995年)。  
  
-   Stegman、 Michael O、 Signore、 Robert 底下和 Creamer，John: *ODBC 方案、 開放式資料庫連接，在分散式環境*（McGraw-山勢阻擋，1995年）。  
  
-   是，Keith:*使用 ODBC 2* （佇列，1994年）。  
  
-   Whiting 帳單：*教導您自己 ODBC 21 天內*(Howard 工時 Sam & 公司，1994年)。
