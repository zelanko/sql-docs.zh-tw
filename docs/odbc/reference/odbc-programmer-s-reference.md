---
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
ms.openlocfilehash: 6a9ca32627b9703465dcfca554fdc32ae01442e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280508"
---
# <a name="odbc-programmer39s-reference"></a>ODBC 程式設計人員&#39;s 參考
ODBC 程式設計*人員參考*包含下列各節。  
  
-   [ODBC 3.8 的新](../../odbc/reference/what-s-new-in-odbc-3-8.md)功能列出 WINDOWS 8 SDK 中新增的 odbc 功能。  
  
-   [範例 Odbc 程式](../../odbc/reference/sample-odbc-program.md)會提供範例 odbc 程式。  
  
-   [Odbc 簡介](../../odbc/reference/introduction-to-odbc.md)提供結構化查詢語言 (SQL) 和 odbc 的簡短歷程記錄，以及有關 odbc 介面的概念資訊。  
  
-   [開發應用程式](../../odbc/reference/develop-app/developing-applications.md)包含開發使用 ODBC 介面的應用程式，以及用來執行它的驅動程式的相關資訊。  
  
-   [安裝和設定 ODBC 軟體](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md)會提供安裝和安裝程式 DLL 函數參考的相關資訊。  
  
-   [開發 ODBC 驅動程式](../../odbc/reference/develop-driver/developing-an-odbc-driver.md)包含有關撰寫驅動程式的資訊。  
  
-   [API 參考](../../odbc/reference/syntax/odbc-reference.md)包含所有 ODBC 函數的語法和語義資訊。  
  
-   [Odbc 附錄](../../odbc/reference/appendixes/odbc-appendixes.md)包含 odbc 錯誤碼、資料類型和 SQL 文法的技術詳細資料和參考資料表。  
  
## <a name="working-with-the-odbc-documentation"></a>使用 ODBC 檔  
 ODBC 介面是專為搭配 C 程式設計語言使用所設計。 ODBC 介面可用於下列三方面︰SQL 陳述式、ODBC 函式呼叫和 C 程式設計。 本檔假設下列各項：  
  
-   C 程式設計語言的實用知識。  
  
-   一般 DBMS 知識和熟悉的 SQL。  
  
 使用下列印刷樣式慣例。  
  
|[格式]|用於|  
|------------|--------------|  
|SELECT * FROM|大寫字母表示用於作業系統命令層級的 SQL 語句、宏名稱和詞彙。|  
|`RETCODE SQLFetch(hdbc)`|等寬字型用於範例命令列和程式碼。|  
|*引數*|斜體單字表示程式設計引數、使用者或應用程式必須提供的資訊，或文字強調。|  
|**SQLEndTran**|粗體類型表示語法必須完全如所示輸入，包括函數名稱。|  
|&#124;|分隔號會分隔語法行中兩個互斥的選項。|  
|...|省略號表示引數可以重複數次。|  
|. . .|具有三個點的資料行會指出先前程式程式碼的接續。|  
  
## <a name="about-the-code-examples"></a>關於程式碼範例  
 本指南中的程式碼範例僅供說明之用。 因為它們主要是用來示範 ODBC 原則，所以有時候會將效率設定為明確的意義。 此外，有時候會省略程式碼的整個區段以清楚說明。 其中包括非 ODBC 函式的定義（名稱不是以 "SQL" 為開頭的函數）和大部分的錯誤處理。  
  
 所有程式碼範例都使用 ANSI 字串和相同的資料庫架構，這會顯示在[目錄](../../odbc/reference/develop-app/catalog-functions.md)函式的開頭。  
  
## <a name="recommended-reading"></a>建議閱讀資料  
 如需 SQL 的詳細資訊，可使用下列標準：  
  
-   具有完整性增強功能的資料庫語言-SQL，ANSI，1989 ANSI X 3.135-1989 年。  
  
-   資料庫語言-SQL： ANSI X3H2 和 ISO/IEC JTC1/SC21/WG3 9075:1992 （SQL-92）。  
  
-   開啟群組，資料管理：結構化查詢語言 (SQL) （SQL）第2版（開啟的群組，1996）。  
  
 除了標準和廠商特定的 SQL 指南以外，許多書籍也會說明 SQL，包括：  
  
-   Date，c. with Darwen，Hugh： *SQL Standard 的指南*（Addison-Wesley，1993）。  
  
-   Emerson、Sandra L.、Darnovsky、Marcy 和 Bowman、Judith S.：實務*SQL 手冊*（Addison-Wesley，1989）。  
  
-   Groff，James R. and Weinberg，Paul N.：*使用 SQL* （Osborne Mcgraw-hill-峰，1990）。  
  
-   Gruber，聖馬丁：*瞭解 SQL* （Sybex，1990）。  
  
-   Hursch、插座 L. 和 Carolyn J.： *SQL、結構化查詢語言 (SQL)* （索引標籤書籍、1988）。  
  
-   Melton、Jim 和 Simon、Alan R。：*瞭解新的 SQL：完整的指南*（Morgan Kaufmann 發行者，1993）。  
  
-   Pascal、Fabian： *SQL 和關聯式基本概念*（M & 的書籍，1990）。  
  
-   Trimble、J Harvey、Jr. 和 Chappell，David： *SQL 的視覺化簡介*（Wiley，1989）。  
  
-   Van der Lan，Rick F.： *SQL 簡介*（Addison-Wesley，1988）。  
  
-   Vang、Soren： *SQL 和關係資料庫*（Microtrend 書籍，1990）。  
  
-   Viescas，John： *SQL 的快速參考指南*（Microsoft Corp.，1989）。  
  
 如需交易處理的詳細資訊，請參閱：  
  
-   灰色、J. N。 和 Reuter，Andreas：*交易處理：概念和技術*（Morgan Kaufmann 發行者，1993）。  
  
-   Hackathorn，Richard d.： *Enterprise Database Connectivity* （Wiley & 兒子，1993）。  
  
 如需呼叫層級介面的詳細資訊，請使用下列標準：  
  
-   開啟群組，*資料管理： SQL 呼叫層級介面（CLI），C451* （開啟群組，1995）。  
  
-   ISO/IEC 9075-3:1995、呼叫層級介面（SQL/CLI）。  
  
 如需有關 ODBC 的其他資訊，有一些書籍可供使用，包括：  
  
-   Geiger，Kyle：*在 ODBC 中*（Microsoft 按®，1995）。  
  
-   Gryphon、Robert、Charpentier、L u c、Oelschlager、Jon、Shoemaker、Andrew、Cross、Jim 和 Lilley、Albert W.：*使用 ODBC 2* （Que，1994）。  
  
-   約翰 Osborne，Mark： *ODBC 開發人員指南*（Howard，& 公司，1994）。  
  
-   北部、Ken： *Windows 多 DBMS 程式設計：使用 c + +、Visual Basic、ODBC、OLE 2 和 Tools FOR DBMS 專案*（John Wiley & 兒子，inc.，1995）。  
  
-   Stegman，Michael O.，Signore，Robert，and Creamer，John： *ODBC 解決方案，在分散式環境中開啟資料庫連接*（Mcgraw-hill-峰，1995）。  
  
-   Welch，Keith：*使用 ODBC 2* （Que，1994）。  
  
-   Whiting，帳單：*在二十天內讓您自己的 ODBC* （Howard，& 公司，1994）。
