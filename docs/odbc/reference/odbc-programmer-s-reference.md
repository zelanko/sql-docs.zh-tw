---
title: ODBC 程式設計人員&#39;參考 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd729956ee7bb1fccf7a8fceb7a435042df4df7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111188"
---
# <a name="odbc-programmer39s-reference"></a>ODBC 程式設計人員&#39;參考
*ODBC 程式設計人員參考*包含下列各節。  
  
-   [What's New in ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md)列出在 Windows 8 SDK 中所新增的新 ODBC 功能。  
  
-   [範例 ODBC 程式](../../odbc/reference/sample-odbc-program.md)提供範例 ODBC 程式。  
  
-   [ODBC 簡介](../../odbc/reference/introduction-to-odbc.md)提供簡短的歷程記錄的結構化查詢語言和 ODBC 和 ODBC 介面的概念性資訊。  
  
-   [開發應用程式](../../odbc/reference/develop-app/developing-applications.md)包含開發使用 ODBC 介面和實作它的驅動程式的應用程式的相關資訊。  
  
-   [安裝和設定 ODBC 軟體](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md)提供安裝和設定 DLL 函式參考的相關資訊。  
  
-   [開發 ODBC 驅動程式](../../odbc/reference/develop-driver/developing-an-odbc-driver.md)包含撰寫驅動程式的相關資訊。  
  
-   [API 參考](../../odbc/reference/syntax/odbc-reference.md)包含的語法和所有的 ODBC 函式的語意資訊。  
  
-   [ODBC 附錄](../../odbc/reference/appendixes/odbc-appendixes.md)包含技術詳細資料，並參考 ODBC 錯誤碼、 資料類型，以及 SQL 文法的資料表。  
  
## <a name="working-with-the-odbc-documentation"></a>使用 ODBC 文件  
 ODBC 介面被設計為搭配 C 程式設計語言。 使用 ODBC 介面跨越三個區域：SQL 陳述式、 ODBC 函式呼叫和 C 程式設計。 這份文件的假設如下：  
  
-   使用 C 程式設計語言的知識。  
  
-   一般 DBMS 知識並熟悉 SQL。  
  
 會使用下列的印刷樣式慣例。  
  
|格式|用於|  
|------------|--------------|  
|選取 * 從|大寫字母會指出 SQL 陳述式、 巨集名稱和作業系統命令層級使用的詞彙。|  
|`RETCODE SQLFetch(hdbc)`|等寬字型用於命令列範例和程式碼而定。|  
|*引數*|斜體的文字表示程式設計的引數，該使用者或應用程式必須提供，或 word 強調的資訊。|  
|**SQLEndTran**|粗體類型表示語法必須完全如下所示，包括函式名稱來輸入。|  
|&#124;|直條會分隔語法列中的兩個互斥的選項。|  
|...|省略符號表示引數可以重複多次。|  
|. . .|三個點的資料行表示先前程式碼行的接續。|  
  
## <a name="about-the-code-examples"></a>關於程式碼範例  
 本指南中的程式碼範例是僅供說明用途設計的。 因為已寫入主要是為了示範 ODBC 原則，效率有時已設定擱置在一旁為了清楚起見。 此外，整個程式碼區段有時為了清楚起見已省略。 這些包括非 ODBC 函數 （其名稱開頭不是 「 SQL 」 那些函式） 和大部分的錯誤處理的定義。  
  
 所有的程式碼範例會使用 ANSI 字串和相同的資料庫結構描述，其會顯示在開頭[目錄函數](../../odbc/reference/develop-app/catalog-functions.md)。  
  
## <a name="recommended-reading"></a>建議閱讀資料  
 如需有關 SQL 的詳細資訊，下列標準可用：  
  
-   資料庫語言-SQL 與完整性的增強功能，ANSI，1989 ANSI X3.135 1989。  
  
-   資料庫語言-SQL:ANSI X3H2 和 ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92)。  
  
-   開啟群組，資料管理：結構化查詢語言 (SQL) 版本 2 (Open Group 1996)。  
  
 除了標準和廠商特定 SQL 輔助線，許多書籍會說明 SQL，包括：  
  
-   日期，C.J.、 Darwen、 Hugh 使用：*SQL 標準的指南*(Addison-Wesley,2005 1993)。  
  
-   Emerson、 Sandra L.、 Darnovsky、 Marcy 和 Bowman，Judith S:*實際 SQL 手冊*(Addison-Wesley,2007，1989年)。  
  
-   Groff、 James R 和 Weinberg，Paul N:*使用 SQL* (兩本書 Mcgraw-hill 1990)。  
  
-   Gruber Martin:*了解 SQL* (Sybex，1990年)。  
  
-   Hursch，Jack L.和林麗莉 J.:*SQL、 結構化的查詢語言*（索引標籤書籍、 1988年）。  
  
-   Melton、 Jim 和 Simon，Alan R:*了解新的 SQL:完整的指南*（Morgan Kaufmann 發行者，1993年）。  
  
-   Pascal 命名法，Fabian:*SQL 與關聯式的基本概念*（M 和 T 書籍，1990年）。  
  
-   Trimble、 J.Harvey，Jr.和 Chappell，David:*觀看式簡介 SQL* (Wiley，1989)。  
  
-   Rick F.van der Lan:*簡介 SQL* (Addison-Wesley,2005 1988)。  
  
-   Vang Soren:*SQL 和關聯式資料庫*（Microtrend 書籍，1990年）。  
  
-   Viescas，John:*SQL 快速參考指南*(Microsoft Corp.1989)。  
  
 如需有關交易處理的詳細資訊，請參閱：  
  
-   Gray, J. N. 和 Reuter，Andreas:*交易處理：概念和技術*（Morgan Kaufmann 發行者，1993年）。  
  
-   Hackathorn，Richard D.:*企業資料庫連線能力*(Wiley & 兒子，1993年)。  
  
 如需有關呼叫層級介面的詳細資訊，下列標準可用：  
  
-   Open Group*資料管理：SQL 呼叫層級介面 (CLI)、 C451* (Open Group 1995 年)。  
  
-   ISO/IEC 9075-3:1995，呼叫層級介面 (SQL/CLI)。  
  
 如需關於 ODBC 的詳細資訊，有多個的書籍，包括：  
  
-   Geiger Kyle:*在 ODBC* (Microsoft Press®，1995 年)。  
  
-   Gryphon、 Robert、 Charpentier、 l u c、 Oelschlager、 Jon、 Shoemaker，Andrew，Jim，跨和 Lilley、 Albert W.:*使用 ODBC 2* （查詢，1994年）。  
  
-   詹斯頓、 Tom 和兩本書標示：*ODBC 的開發人員指南*（Howard W.Sams 和公司，1994年）。  
  
-   北美，Ken:*Windows 多 DBMS 程式設計：使用C++，Visual Basic、 ODBC、 OLE 2 和適用於 DBMS 專案工具*(John Wiley & 兒子，Inc.，1995 年)。  
  
-   Stegman、 Michael O.、 Signore、 Robert 和 Creamer，John:*ODBC 解決方案、 開放式資料庫連接，在分散式環境*(Mcgraw-hill 1995 年)。  
  
-   Edsby Keith:*使用 ODBC 2* （查詢，1994年）。  
  
-   Whiting，帳單：*自學 ODBC 在 21 天內*（Howard W.Sams 和公司，1994年）。
