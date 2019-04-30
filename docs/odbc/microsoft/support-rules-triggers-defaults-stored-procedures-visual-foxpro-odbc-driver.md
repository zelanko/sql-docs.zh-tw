---
title: 支援的規則、 觸發程序、 預設值和預存程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], stored procedures
- FoxPro ODBC driver [ODBC], commands and functions
- commands for FoxPro ODBC driver [ODBC]
- FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], triggers
- stored procedures [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], rules
- FoxPro commands and functions [ODBC]
- rules [ODBC]
- Visual FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], rules
- functions [ODBC], Visual FoxPro
- default values [ODBC]
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro ODBC driver [ODBC], triggers
- FoxPro ODBC driver [ODBC], stored procedures
- Visual FoxPro commands and functions [ODBC]
ms.assetid: e449de20-d6ca-4902-9f8e-814eb6e86650
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47795998b019df22b01852519f75f6e8d3d274dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269870"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>規則、觸發程序、預設值和預存程序支援 (Visual FoxPro ODBC Driver)
您無法建立 Visual FoxPro 規則、 觸發程序、 預設值或使用 Visual FoxPro ODBC Driver 的預存程序。 不過，您的應用程式可能互動與現有的規則、 觸發程序、 預設值或預存程序中，因為它會插入、 更新或刪除 Visual FoxPro 資料儲存在資料庫中。  
  
 下表列出的 Visual FoxPro 命令和命令或函式存在於規則、 觸發程序、 預設值或預存程序時，Visual FoxPro ODBC Driver 所支援的函式。  
  
 如果您的應用程式互動資料的規則、 觸發程序、 預設值，或任何其他的 Visual FoxPro 命令或函式，呼叫預存程序，驅動程式會產生錯誤。 請參閱[不支援的 Visual FoxPro 命令和函式](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md)如需命令和驅動程式不支援的函式的清單。  
  
> [!TIP]  
>  如果您想要將條件式的程式碼插入您的規則、 觸發程序或預存程序可決定要呼叫由驅動程式時所執行的命令，您可以使用**版本 （)** 函式。 **版本 （)** 函式會傳回 「 Visual FoxPro ODBC Driver *\<版本 >*」 驅動程式呼叫時。  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Visual FoxPro 命令和規則、 觸發程序、 預設值和預存程序中支援的函式  
  
||||  
|-|-|-|  
|$ 運算子|%運算子|（& s) 命令|  
|& & 命令|* 命令|= 命令|  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ABS （） 函式|有權自行決定 （） 函式|新增資料表 命令|  
|ADATABASES （） 函式|ADBOBJECTS （） 函式|AERROR （） 函式|  
|ADEL （） 函式|AELEMENT （） 函式|ALEN （） 函式|  
|AFIELDS （） 函式|AINS （） 函式|ALTER TABLE - SQL 命令|  
|別名 （） 函式|ALLTRIM （） 函式|附加從陣列命令|  
|AND 運算子|附加命令|新增備忘 命令|  
|附加命令|附加一般命令|ASCAN （） 函式|  
|附加程序命令|ASC （） 函式|ASUBSCRIPT （） 函式|  
|ASIN （） 函式|ASORT （） 函式|ATAN （） 函式|  
|（） 函式|AT_C （） 函式|ATCLINE （） 函式|  
|ATC （） 函式|ATCC （） 函式|AUSED （） 函式|  
|ATLINE （） 函式|ATN2 （） 函式||  
|平均命令|ACOS （） 函式||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|開始交易命令|之間 （） 函式|BITNOT （） 函式|  
|BITCLEAR （） 函式|BITLSHIFT （） 函式|BITSET （） 函式|  
|BITOR （） 函式|BITRSHIFT （） 函式|空白的命令|  
|位元測試 （） 函式|BITXOR （） 函式||  
|BOF （） 函式|BITAND （） 函式||  
  
## <a name="c"></a>c  
  
||||  
|-|-|-|  
|計算命令|候選版 （） 函式|CHR （） 函式|  
|CDX （） 函式|CEILING （） 函式|關閉命令|  
|CHRTRAN （） 函式|CHRTRANC （） 函式|索引 [複製] 命令|  
|CMONTH （） 函式|繼續命令|複製結構擴充命令|  
|複製程序命令|複製 [結構] 命令|將複製到命令|  
|複製 [標記] 命令|將複製到陣列命令|CPCONVERT （） 函式|  
|COS （） 函式|COUNT 命令|CTOD （） 函式|  
|CPCURRENT （） 函式|CPDBF （） 函式|CURSORSETPROP （） 函式|  
|CTOT （） 函式|CURSORGETPROP （） 函式||  
|CURVAL （） 函式|CDOW （） 函式||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|DATE （） 函式|DATETIME （） 函式|DAY （） 函式|  
|雙位元組字元 （） 函式|DBF （） 函式|DBGETPROP （） 函式|  
|DBUSED （） 函式|DELETE - SQL 命令|刪除命令|  
|DELETE TAG 命令|已刪除 （） 函式|遞減 （） 函式|  
|差異 （） 函式|維度命令|磁碟空間 （） 函式|  
|DMY （） 函式|執行案例...ENDCASE 命令|命令|  
|時...ENDDO 命令|DOW （） 函式|DTOC （） 函式|  
|DTOR （） 函式|DTO （） 函式|DTOT （） 函式|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|空的 （） 函式|評估 （） 函式|EXIT 命令|  
|錯誤 （） 函式|EXP （） 函式||  
|結束交易的命令|EOF （） 函式||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|FCOUNT （） 函式|FDATE （） 函式|欄位 （） 函式|  
|檔案 （） 函式|篩選 （） 函式|FLDLIST （） 函式|  
|FLOCK （） 函式|FLOOR （） 函式|排清的命令|  
|FOR...ENDFOR 命令|（） 函式|找到 （） 函式|  
|可用的資料表 命令|FSIZE （） 函式|FTIME （） 函式|  
|FULLPATH （） 函式|函式命令|FV （） 函式|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|收集命令|GETNEXTMODIFIED （） 函式|移至/GOTO 命令|  
|GETFLDSTATE （） 函式|GOMONTH （） 函式||  
|GETCP （） 函式|GETENV （） 函式||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|標頭 > （） 函式|小時 （） 函式|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE （） 函式|IF...ENDIF 命令|IIF （） 函式|  
|INDBC （） 函式|INDEX 命令|INLIST （） 函式|  
|INSERT SQL 命令|INT （） 函式|ISALPHA （） 函式|  
|ISBLANK （） 函式|ISDIGIT （） 函式|ISEXCLUSIVE （） 函式|  
|ISLEADBYTE （） 函式|ISLOWER （） 函式|ISNULL （） 函式|  
|ISREADONLY （） 函式|ISUPPER （） 函式||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|索引鍵 （） 函式|KEYMATCH （） 函式||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|左 （） 函式|LEFTC （） 函式|LIKEC （） 函式|  
|LENC （） 函式|例如 （） 函式|LOCK （） 函式|  
|本機命令|尋找命令|查閱 （） 函式|  
|記錄檔 （） 函式|LOG10 （） 函式|LTRIM （） 函式|  
|LOWER （） 函數|LPARAMETERS 命令||  
|LUPDATE （） 函式|LEN （） 函式||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE 系統記憶體變數|MAX （） 函式|MDX （） 函式|  
|MDY （） 函式|MEMLINES （） 函式|訊息 （） 函式|  
|MIN （） 函式|每分鐘 （） 函式|MLINE （） 函式|  
|MOD （） 函式|月 （） 函式|MTON （） 函式|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NDX （） 函式|正規化 （） 函式|NOT 運算子|  
|請注意命令|NTOM （） 函式|NVL （） 函式|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|（） 函式，就會發生|OLDVAL （） 函式|在錯誤的命令|  
|索引鍵的命令|（） 函式|開啟的資料庫命令|  
|OR 運算子|順序 （） 函式|OS （） 函式|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|套件命令|參數 （） 函式|付款 （） 函式|  
|參數的命令|主要 （） 函式|私用的命令|  
|PI （） 函式|程式 （） 函式|適當的 （） 函式|  
|程序命令|PV （） 函式||  
|公用的命令|PADL( ) &#124; PADR( ) &#124; PADC( ) Functions||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|RAND （） 函式|RAT （） 函式|RATC （） 函式|  
|RATLINE （） 函式|重新叫用命令|RECCOUNT （） 函式|  
|RECNO （） 函式|RECSIZE （） 函式|區域的命令|  
|關聯性 （） 函式|移除資料表 命令|取代命令|  
|取代陣列命令|REPLICATE （） 函式|重試命令|  
|傳回命令|右 （） 函式|RIGHTC （） 函式|  
|RLOCK （） 函式|回復命令|ROUND （） 函式|  
|RTOD （） 函式|RTRIM （） 函式||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|掃描...ENDSCAN 命令|散佈圖命令|秒 （） 函式|  
|秒 （） 函式|搜尋命令|搜尋 （） 函式|  
|選取命令|選取 （） 函式|選取 SQL 命令|  
|SET BLOCKSIZE 命令|集合所包含的命令|SET 世紀命令|  
|SET COLLATE 命令|SET 資料庫命令|SET 日期命令|  
|設定預設的命令|SET DELETED 命令|SET EXACT 命令|  
|SET EXCLUSIVE 命令|SET FDOW 命令|SET 欄位命令|  
|SET 篩選命令|設定固定的命令|SET FULLPATH 命令|  
|SET FWEEK 命令|設定的小時命令|SET 索引命令|  
|SET LOCK 命令|SET MULTILOCKS 命令|接近命令設定|  
|SET NOCPTRANS 命令|設定通知命令|SET NULL 命令|  
|SET 最佳化命令|SET 順序命令|SET PATH 命令|  
|SET 程序命令|設定關聯的命令|設定關聯 OFF 命令|  
|SET REPROCESS 命令|設定略過命令|SET UDFPARMS 命令|  
|SET UNIQUE 命令|設定磁碟區命令|SET （） 函式|  
|SETFLDSTATE （） 函式|SIGN （） 函式|SIN （） 函式|  
|略過命令|排序命令|空間 > （） 函式|  
|SQRT （） 函式|存放區命令|STR （） 函式|  
|STRCONV （） 函式|STRTRAN （） 函式|STUFF （） 函數|  
|STUFFC （） 函式|SUBSTR （） 函式|SUBSTRC （） 函式|  
|加總 命令|SYS(2011) 函式||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY 系統記憶體變數|_TRIGGERLEVEL 系統記憶體變數|TAGCOUNT （） 函式|  
|TABLEUPDATE （） 函式|標記 （） 函式|目標 （） 函式|  
|TAGNO （） 函式|TAN （） 函式|修剪 （） 函式|  
|時間 （） 函式|總命令|TXNLEVEL （） 函式|  
|TTOC （） 函式|TTOD （） 函式||  
|型別 （） 函式|TABLEREVERT （） 函式||  
  
## <a name="u"></a>u  
  
||||  
|-|-|-|  
|唯一的 （） 函式|UNLOCK 命令|使用命令|  
|UPDATE 命令|上方的 （） 函式||  
|使用 （） 函式|UPDATE - SQL 命令||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL （） 函式|版本 （） 函式||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|週 （） 函式|||  
  
## <a name="y"></a>Y  
  
||||  
|-|-|-|  
|YEAR （） 函式|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZAP 命令|||
