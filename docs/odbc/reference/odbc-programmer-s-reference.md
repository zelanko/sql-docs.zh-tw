---
title: ODBC 程式師&#39;參考 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280508"
---
# <a name="odbc-programmer39s-reference"></a>ODBC 程式師&#39;參考
*ODBC 程式師的參考*包含以下部分。  
  
-   [ODBC 3.8 中的新增](../../odbc/reference/what-s-new-in-odbc-3-8.md)功能列出了 Windows 8 SDK 中添加的新 ODBC 功能。  
  
-   [示例ODBC計劃](../../odbc/reference/sample-odbc-program.md)提供了ODBC計劃範例。  
  
-   [ODBC 簡介](../../odbc/reference/introduction-to-odbc.md)提供了結構化查詢語言和 ODBC 的簡要歷史記錄,以及有關 ODBC 介面的概念資訊。  
  
-   [開發應用程式](../../odbc/reference/develop-app/developing-applications.md)包含有關開發使用 ODBC 介面的應用程式的資訊以及實現該應用程式的驅動程式。  
  
-   [安裝和配置 ODBC 軟體](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md)提供有關安裝的資訊和設置 DLL 功能參考。  
  
-   [開發 ODBC 驅動程式](../../odbc/reference/develop-driver/developing-an-odbc-driver.md)包含有關編寫驅動程式的資訊。  
  
-   [API 參考](../../odbc/reference/syntax/odbc-reference.md)包含所有 ODBC 函數的語法和語義資訊。  
  
-   [ODBC 附錄](../../odbc/reference/appendixes/odbc-appendixes.md)包含 ODBC 錯誤代碼、數據類型和 SQL 語法的技術詳細資訊和參考表。  
  
## <a name="working-with-the-odbc-documentation"></a>使用 ODBC 文件  
 ODBC 介面是專為搭配 C 程式設計語言使用所設計。 ODBC 介面可用於下列三方面︰SQL 陳述式、ODBC 函式呼叫和 C 程式設計。 此文件的字列以下內容:  
  
-   C程式設計語言的工作知識。  
  
-   一般 DBMS 知識和對 SQL 的熟悉程度。  
  
 使用以下排版約定。  
  
|[格式]|用於|  
|------------|--------------|  
|選擇 = 從|大寫字母表示 SQL 語句、宏名稱和在作業系統命令級別使用的術語。|  
|`RETCODE SQLFetch(hdbc)`|單一空間字體用於示例命令行和程式代碼。|  
|*引數*|斜體字表示程式設計參數、使用者或應用程式必須提供的資訊或單詞強調。|  
|**SQLEndTran**|粗體類型表示語法必須完全按照所示類型進行鍵入,包括函數名稱。|  
|&#124;|垂直條分隔語法行中的兩個互斥選項。|  
|...|省略號表示參數可以重複多次。|  
|. . .|三個點的列表示前幾行代碼的延續。|  
  
## <a name="about-the-code-examples"></a>關於代碼範例  
 本指南中的代碼示例僅用於說明目的。 因為它們主要是為了展示ODBC原則,因此有時為了明確起見,效率被擱置一邊。 此外,為了清楚起見,有時省略了代碼的整個部分。 其中包括非 ODBC 函數(名稱不以"SQL"開頭的函數)和大多數錯誤處理的定義。  
  
 所有代碼示例都使用 ANSI 字串和相同的資料庫架構,這在[目錄函數](../../odbc/reference/develop-app/catalog-functions.md)的開頭顯示。  
  
## <a name="recommended-reading"></a>建議閱讀資料  
 有關 SQL 的詳細資訊,可以使用以下標準:  
  
-   資料庫語言 - 具有完整性增強的 SQL,ANSI,1989 ANSI X3.135-1989。  
  
-   資料庫語言 - SQL:ANSI X3H2 和 ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92)。  
  
-   開放組,數據管理:結構化查詢語言(SQL),版本 2(開放組,1996 年)。  
  
 除了標準和特定於供應商的 SQL 指南外,許多書籍還描述了 SQL,包括:  
  
-   日期,C.J.,達文,休 *:SQL標準指南*(艾迪森-韋斯利,1993年)。  
  
-   艾默生、桑德拉·L、達諾夫斯基、馬西和鮑曼,裘蒂思:*實用SQL手冊*(艾迪森-韋斯利,1989年)。  
  
-   格羅夫,詹姆斯R.和文伯格,保羅N.:*使用SQL(* 奧斯本麥格勞希爾,1990年)。  
  
-   格魯伯,馬丁:*理解*SQL(Sybex,1990年)。  
  
-   赫爾施,傑克L.和卡羅琳*J.:SQL,結構化查詢語言*(TAB書籍,1988年)。  
  
-   梅爾頓、吉姆和西蒙,艾倫:*瞭解新的SQL:一個完整的指南*(摩根考夫曼出版社,1993年)。  
  
-   帕斯卡爾,法比安 *:SQL和關係基礎知識*(M&T書籍,1990年)。  
  
-   特林布爾,小J.哈威和查佩爾,大衛 *:SQL的視覺介紹*(威利,1989年)。  
  
-   范德蘭斯,里克*F.:SQL簡介*(艾迪森-韋斯利,1988年)。  
  
-   Vang, 索倫 *:SQL 和關係資料庫*(微趨勢書籍,1990 年)。  
  
-   約翰·維斯卡斯 *:SQL 快速參考指南*(微軟公司,1989 年)。  
  
 有關事務處理的其他資訊,請參閱:  
  
-   格雷,J.N. 和Reuter,Andreas:*交易處理:概念和技術*(摩根·考夫曼出版社,1993年)。  
  
-   哈克索恩,理查德D.:*企業資料庫連接*(威利&兒子,1993年)。  
  
 有關呼叫層介面的詳細資訊,請提供以下標準:  
  
-   打開組,*資料管理:SQL 呼叫等級介面 (CLI),C451(* 開放組,1995 年)。  
  
-   ISO/IEC 9075-3:1995,呼叫級介面(SQL/CLI)。  
  
 有關 ODBC 的更多資訊,可查閱多本書,包括:  
  
-   蓋格,凱爾 *:ODBC內部*(微軟出版社®,1995年)。  
  
-   格裡芬,羅伯特,查彭蒂埃,呂克,歐爾施拉格,喬恩,鞋匠,安德魯,克羅斯,吉姆和利利,阿爾伯特W.:*使用ODBC* 2(Que,1994年)。  
  
-   約翰斯頓,湯姆和奧斯本,馬克 *:ODBC開發者指南*(霍華德·薩姆斯&公司,1994年)。  
  
-   北,肯 *:Windows多DBMS程式設計:使用C++、視覺基礎、ODBC、OLE 2 和 DBMS 專案工具*(John Wiley & Sons, Inc.,1995 年)。  
  
-   斯特格曼、邁克爾·奧、索多洛、羅伯特和梅勒,約翰 *:ODBC 解決方案,分散式環境中的開放資料庫連接*(McGraw-Hill,1995 年)。  
  
-   韋爾奇,基思:*使用ODBC* 2(Que,1994年)。  
  
-   惠廷,比爾:*在二十一天內自學ODBC(* 霍華德·薩姆斯&公司,1994年)。
