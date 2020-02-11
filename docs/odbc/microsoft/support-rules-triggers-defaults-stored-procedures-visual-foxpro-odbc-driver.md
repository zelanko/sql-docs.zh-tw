---
title: 支援規則、觸發程式、預設值和預存程式 |Microsoft Docs
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
ms.openlocfilehash: 90a39ad540f3320ed78e981030679b59d911eeef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68080768"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>規則、觸發程序、預設值和預存程序支援 (Visual FoxPro ODBC Driver)
您無法使用 Visual FoxPro ODBC Driver 來建立 Visual FoxPro 規則、觸發程式、預設值或預存程式。 不過，您的應用程式可能會在插入、更新或刪除儲存在資料庫中的 Visual FoxPro 資料時，與現有的規則、觸發程式、預設值或預存程式互動。  
  
 下表列出當規則、觸發程式、預設值或預存程式中有命令或函式時，Visual FoxPro ODBC Driver 所支援的 Visual FoxPro 命令和函式。  
  
 如果您的應用程式與規則、觸發程式、預設值或預存程式呼叫任何其他 Visual FoxPro 命令或函數的資料互動，驅動程式會產生錯誤。 如需驅動程式不支援的命令和功能清單，請參閱[不支援的 Visual FoxPro 命令和](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md)函式。  
  
> [!TIP]  
>  如果您想要將條件式程式碼插入規則、觸發程式或預存程式，以判斷驅動程式呼叫時要執行的命令，您可以使用**VERSION （）** 函數。 **VERSION （）** 函式會在驅動程式呼叫時傳回「Visual FoxPro ODBC Driver * \<VERSION>*」。  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>規則、觸發程式、預設值和預存程式中支援的 Visual FoxPro 命令和函式  
  
||||  
|-|-|-|  
|$ 運算子|% 運算子|& 命令|  
|&& 命令|* 命令|= 命令|  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ABS （）函數|ACOPY （）函數|新增資料表命令|  
|ADATABASES （）函數|ADBOBJECTS （）函數|AERROR （）函數|  
|ADEL （）函數|AELEMENT （）函數|ALEN （）函數|  
|AFIELDS （）函數|AINS （）函數|ALTER TABLE - SQL 命令|  
|ALIAS （）函數|ALLTRIM （）函數|從陣列附加命令|  
|AND 運算子|APPEND 命令|附加備忘命令|  
|從命令附加|附加一般命令|ASCAN （）函數|  
|附加程式命令|ASC （）函數|ASUBSCRIPT （）函數|  
|ASIN （）函數|ASORT （）函數|ATAN （）函數|  
|AT （）函數|AT_C （）函數|ATCLINE （）函數|  
|ATC （）函數|ATCC （）函數|AUSED （）函數|  
|ATLINE （）函數|ATN2 （）函數||  
|平均命令|ACOS （）函數||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|BEGIN TRANSACTION 命令|BETWEEN （）函數|BITNOT （）函數|  
|BITCLEAR （）函數|BITLSHIFT （）函數|BITSET （）函數|  
|BITOR （）函數|BITRSHIFT （）函數|空白命令|  
|BITTEST （）函數|BITXOR （）函數||  
|BOF （）函數|BITAND （）函數||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|計算命令|候選（）函數|CHR （）函數|  
|CDX （）函數|上限（）函數|關閉命令|  
|CHRTRAN （）函數|CHRTRANC （）函數|複製索引命令|  
|CMONTH （）函數|繼續命令|複製結構擴充命令|  
|複製程式命令|複製結構命令|複製到命令|  
|複製標記命令|複製到陣列命令|CPCONVERT （）函數|  
|COS （）函數|COUNT 命令|CTOD （）函數|  
|CPCURRENT （）函數|CPDBF （）函數|CURSORSETPROP （）函數|  
|CTOT （）函數|CURSORGETPROP （）函數||  
|CURVAL （）函數|CDOW （）函數||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|DATE （）函數|DATETIME （）函數|DAY （）函數|  
|DBC （）函數|DBF （）函數|DBGETPROP （）函數|  
|DBUSED （）函數|DELETE - SQL 命令|DELETE 命令|  
|DELETE TAG 命令|DELETED （）函數|遞減（）函數|  
|差異（）函數|維度命令|磁碟空間（）函數|  
|DMY （）函數|執行案例 .。。ENDCASE 命令|DO 命令|  
|執行時間 .。。ENDDO 命令|DOW （）函數|DTOC （）函數|  
|DTOR （）函數|DTO （）函數|DTOT （）函數|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|EMPTY （）函數|評估（）函數|EXIT 命令|  
|ERROR （）函式|EXP （）函數||  
|結束交易命令|EOF （）函數||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|FCOUNT （）函數|FDATE （）函數|FIELD （）函數|  
|FILE （）函數|FILTER （）函數|FLDLIST （）函數|  
|FLOCK （）函數|FLOOR （）函數|FLUSH 命令|  
|針對 .。。FOR...ENDFOR 命令|FOR （）函數|找到（）函數|  
|免費資料表命令|FSIZE （）函數|FTIME （）函數|  
|FULLPATH （）函數|FUNCTION 命令|FV （）函數|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|收集命令|GETNEXTMODIFIED （）函數|GO/GOTO 命令|  
|GETFLDSTATE （）函數|GOMONTH （）函數||  
|GETCP （）函數|GETENV （）函數||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|HEADER （）函數|HOUR （）函數|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE （）函數|如果 .。。ENDIF 命令|IIF （）函數|  
|INDBC （）函數|INDEX 命令|INLIST （）函數|  
|INSERT-SQL 命令|INT （）函數|ISALPHA （）函數|  
|ISBLANK （）函數|ISDIGIT （）函數|ISEXCLUSIVE （）函數|  
|ISLEADBYTE （）函數|ISLOWER （）函數|ISNull （）函數|  
|ISREADONLY （）函數|ISUPPER （）函數||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|KEY （）函數|KEYMATCH （）函數||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|LEFT （）函數|LEFTC （）函數|LIKEC （）函數|  
|LENC （）函數|LIKE （）函數|LOCK （）函數|  
|本機命令|尋找命令|LOOKUP （）函數|  
|LOG （）函數|LOG10 （）函數|LTRIM （）函數|  
|LOWER （）函數|LPARAMETERS 命令||  
|LUPDATE （）函數|LEN （）函數||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE 系統記憶體變數|MAX （）函數|MDX （）函數|  
|MDY （）函數|MEMLINES （）函數|MESSAGE （）函數|  
|MIN （）函數|MINUTE （）函數|MLINE （）函數|  
|MOD （）函數|MONTH （）函數|MTON （）函數|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NDX （）函數|正規化（）函數|NOT 運算子|  
|注意命令|NTOM （）函數|NVL （）函數|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|發生時間（）函數|OLDVAL （）函數|ON ERROR 命令|  
|ON KEY 命令|ON （）函數|開啟資料庫命令|  
|OR 運算子|ORDER （）函數|OS （）函數|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|PACK 命令|PARAMETERS （）函數|付款（）函數|  
|PARAMETERS 命令|PRIMARY （）函數|私用命令|  
|PI （）函數|PROGRAM （）函數|適當的（）函數|  
|程式命令|PV （）函數||  
|公用命令|PADL （） &#124; PADR （） &#124; PADC （）函數||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|RAND （）函數|RAT （）函數|RATC （）函數|  
|RATLINE （）函數|重新叫用命令|RECCOUNT （）函數|  
|RECNO （）函數|RECSIZE （）函數|地區命令|  
|RELATION （）函數|移除資料表命令|REPLACE 命令|  
|[從陣列取代] 命令|複寫（）函數|重試命令|  
|RETURN 命令|RIGHT （）函數|RIGHTC （）函數|  
|RLOCK （）函數|ROLLBACK 命令|ROUND （）函數|  
|RTOD （）函數|RTRIM （）函數||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|掃描 .。。ENDSCAN 命令|散佈命令|SEC （）函數|  
|SECONDS （）函數|搜尋命令|SEEK （）函數|  
|選取命令|SELECT （）函數|SELECT-SQL 命令|  
|SET BLOCKSIZE 命令|設定執行命令|設定世紀命令|  
|SET COLLATE 命令|設定資料庫命令|設定日期命令|  
|設定預設命令|SET DELETED 命令|SET EXACT 命令|  
|SET EXCLUSIVE 命令|SET FDOW 命令|設定欄位命令|  
|設定篩選命令|設定固定的命令|SET FULLPATH 命令|  
|SET FWEEK 命令|設定時數命令|設定索引命令|  
|設定鎖定命令|SET MULTILOCKS 命令|設定 NEAR 命令|  
|SET NOCPTRANS 命令|設定通知命令|SET NULL 命令|  
|設定 OPTIMIZE 命令|設定順序命令|SET PATH 命令|  
|SET PROCEDURE 命令|設定關聯命令|設定關聯關閉命令|  
|SET REPROCESS 命令|設定略過命令|SET UDFPARMS 命令|  
|SET UNIQUE 命令|設定磁片區命令|SET （）函數|  
|SETFLDSTATE （）函數|SIGN （）函數|SIN （）函數|  
|SKIP 命令|SORT 命令|SPACE （）函數|  
|SQRT （）函數|STORE 命令|STR （）函數|  
|STRCONV （）函數|STRTRAN （）函數|事物（）函數|  
|STUFFC （）函數|SUBSTR （）函數|SUBSTRC （）函數|  
|SUM 命令|SYS （2011）函數||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY 系統記憶體變數|_TRIGGERLEVEL 系統記憶體變數|TAGCOUNT （）函數|  
|TABLEUPDATE （）函數|TAG （）函數|TARGET （）函數|  
|TAGNO （）函數|TAN （）函數|TRIM （）函數|  
|TIME （）函數|TOTAL 命令|TXNLEVEL （）函數|  
|TTOC （）函數|TTOD （）函數||  
|TYPE （）函數|TABLEREVERT （）函數||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|UNIQUE （）函數|UNLOCK 命令|使用命令|  
|UPDATE 命令|UPPER （）函數||  
|USED （）函數|UPDATE - SQL 命令||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL （）函數|VERSION （）函數||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|WEEK （）函數|||  
  
## <a name="y"></a>Y  
  
||||  
|-|-|-|  
|YEAR （）函數|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZAP 命令|||
