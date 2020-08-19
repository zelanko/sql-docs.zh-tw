---
description: 規則、觸發程序、預設值和預存程序支援 (Visual FoxPro ODBC Driver)
title: 規則、觸發程式、預設值和預存程式的支援 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56b1a2e50f26da8ce5ef581f8eda7c6a96afd741
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449110"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>規則、觸發程序、預設值和預存程序支援 (Visual FoxPro ODBC Driver)
您無法使用 Visual FoxPro ODBC 驅動程式來建立 Visual FoxPro 規則、觸發程式、預設值或預存程式。 不過，您的應用程式可能會在插入、更新或刪除儲存在資料庫中的 Visual FoxPro 資料時，與現有的規則、觸發程式、預設值或預存程式互動。  
  
 下表列出當規則、觸發程式、預設值或預存程式中有命令或函式時，Visual FoxPro ODBC 驅動程式所支援的 Visual FoxPro 命令和函式。  
  
 如果您的應用程式與其規則、觸發程式、預設值或預存程式呼叫任何其他 Visual FoxPro 命令或函數的資料互動，驅動程式會產生錯誤。 請參閱不 [支援的 Visual FoxPro 命令和](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) 函式，以取得驅動程式不支援的命令和函式清單。  
  
> [!TIP]  
>  如果您想要在規則、觸發程式或預存程式中插入條件式程式碼，以決定驅動程式呼叫時所要執行的命令，您可以使用 **版本 ( ) ** 函式。 此 **版本 ( ) ** 函式會 *\<version>* 在驅動程式呼叫時傳回「Visual FoxPro ODBC 驅動程式」。  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>規則、觸發程式、預設值和預存程式中支援的 Visual FoxPro 命令和函數  

:::row:::
    :::column:::
        $ 運算子  
        % 運算子  
    :::column-end:::
    :::column:::
        & 命令  
        && 命令  
    :::column-end:::
    :::column:::
        \* 命令  
        = 命令  
    :::column-end:::
:::row-end:::

## <a name="a"></a>A  

:::row:::
    :::column:::
        ABS ( ) 函數  
        ACOPY ( ) 函式  
        ACOS ( ) 函式  
        ADATABASES ( ) 函式  
        ADBOBJECTS ( ) 函式  
        加入資料表命令  
        ADEL ( ) 函式  
        AELEMENT ( ) 函式  
        AERROR ( ) 函式  
        AFIELDS ( ) 函式  
        AINS ( ) 函式  
        ALEN ( ) 函式  
        別名 ( ) 函式  
    :::column-end:::
    :::column:::
        ALLTRIM ( ) 函式  
        ALTER TABLE - SQL 命令  
        AND 運算子  
        APPEND 命令  
        從命令附加  
        從陣列命令附加  
        附加一般命令  
        附加備忘錄命令  
        APPEND 程式命令  
        ASC ( ) 函式  
        ) 可以 ( ) 函式  
        ASIN ( ) 函式  
        ASORT ( ) 函式  
    :::column-end:::
    :::column:::
        ASUBSCRIPT ( ) 函式  
        在 ( ) 函式  
        AT_C ( ) 函數  
        ATAN ( ) 函式  
        ATC ( ) 函式  
        ATCC ( ) 函式  
        ATCLINE ( ) 函式  
        ATLINE ( ) 函式  
        ATN2 ( ) 函式  
        AUSED ( ) 函式  
        AVERAGE 命令  
    :::column-end:::
:::row-end:::

## <a name="b"></a>B  

:::row:::
    :::column:::
        BEGIN TRANSACTION 命令  
         ( ) 函數之間  
        BITAND ( ) 函式  
        BITCLEAR ( ) 函式  
        BITLSHIFT ( ) 函式  
    :::column-end:::
    :::column:::
        BITNOT ( ) 函式  
        BITOR ( ) 函式  
        BITRSHIFT ( ) 函式  
        BITSET ( ) 函式  
        BITTEST ( ) 函式  
    :::column-end:::
    :::column:::
        BITXOR ( ) 函式  
        空白命令  
         ( ) 函數的 BOF  
    :::column-end:::
:::row-end:::

## <a name="c"></a>C  

:::row:::
    :::column:::
        計算命令  
        候選 ( ) 函式  
        CDOW ( ) 函式  
        CDX ( ) 函式  
        ) 函數的上限 (  
        CHR ( ) 函數  
        CHRTRAN ( ) 函式  
        CHRTRANC ( ) 函式  
        關閉命令  
        CMONTH ( ) 函式  
    :::column-end:::
    :::column:::
        CONTINUE 命令  
        複製索引命令  
        複製程式命令  
        複製結構命令  
        複製結構擴充命令  
        複製標記命令  
        複製到命令  
        複製到陣列命令  
        COS ( ) 函數  
        COUNT 命令  
    :::column-end:::
    :::column:::
        CPCONVERT ( ) 函式  
        CPCURRENT ( ) 函式  
        CPDBF ( ) 函式  
        CTOD ( ) 函式  
        CTOT ( ) 函式  
        CURSORGETPROP ( ) 函式  
        CURSORSETPROP ( ) 函式  
        CURVAL ( ) 函式  
    :::column-end:::
:::row-end:::

## <a name="d"></a>D  

:::row:::
    :::column:::
        日期 ( ) 函數  
        DATETIME ( ) 函數  
        DAY ( ) 函數  
        DBC ( ) 函式  
        DBF ( ) 函式  
        DBGETPROP ( ) 函式  
        DBUSED ( ) 函式  
        DELETE - SQL 命令  
    :::column-end:::
    :::column:::
        DELETE 命令  
        DELETE TAG 命令  
        已刪除 ( ) 函數  
         ( ) 函數遞減  
         ( ) 函數的差異  
        DIMENSION 命令  
        磁碟空間 ( ) 函式  
        DMY ( ) 函式  
    :::column-end:::
    :::column:::
        DO 命令  
        DO CASE .。。ENDCASE 命令  
        DO WHILE .。。ENDDO 命令  
        DOW ( ) 函式  
        DTOC ( ) 函式  
        DTOR ( ) 函式  
        DTO ( ) 函式  
        DTOT ( ) 函式  
    :::column-end:::
:::row-end:::

## <a name="e"></a>E  

:::row:::
    :::column:::
        空白 ( ) 函式  
        結束交易命令  
        EOF ( ) 函數  
    :::column-end:::
    :::column:::
        ) 函數 ( 時發生錯誤  
        評估 ( ) 函數  
        EXIT 命令  
    :::column-end:::
    :::column:::
        EXP ( ) 函數  
    :::column-end:::
:::row-end:::

## <a name="f"></a>F  

:::row:::
    :::column:::
        FCOUNT ( ) 函式  
        FDATE ( ) 函式  
        欄位 ( ) 函數  
        FILE ( ) 函式  
        篩選 ( ) 函數  
        FLDLIST ( ) 函式  
    :::column-end:::
    :::column:::
        FLOCK ( ) 函式  
        樓層 ( ) 函式  
        FLUSH 命令  
        針對 ( ) 函數  
        適用于 .。。TURTLE 命令  
        找到 ( ) 函式  
    :::column-end:::
    :::column:::
        FREE TABLE 命令  
        FSIZE ( ) 函式  
        FTIME ( ) 函式  
        FULLPATH ( ) 函式  
        函數命令  
        FV ( ) 函數  
    :::column-end:::
:::row-end:::

## <a name="g"></a>G  

:::row:::
    :::column:::
        搜集命令  
        GETCP ( ) 函式  
        GETENV ( ) 函式  
    :::column-end:::
    :::column:::
        GETFLDSTATE ( ) 函式  
        GETNEXTMODIFIED ( ) 函式  
        GO/GOTO 命令  
    :::column-end:::
    :::column:::
        GOMONTH ( ) 函式  
    :::column-end:::
:::row-end:::

## <a name="h"></a>H  

:::row:::
    :::column:::
        標頭 ( ) 函式
    :::column-end:::
    :::column:::
        小時 ( ) 函式
    :::column-end:::
:::row-end:::

## <a name="i"></a>I  

:::row:::
    :::column:::
        IDXCOLLATE ( ) 函式  
        如果。。。ENDIF 命令  
        IIF ( ) 函數  
        INDBC ( ) 函式  
        INDEX 命令  
        數值 INLIST 函數 ( ) 函式  
    :::column-end:::
    :::column:::
        INSERT-SQL 命令  
        INT ( ) 函數  
        ISALPHA ( ) 函式  
        ISBLANK ( ) 函式  
        ISDIGIT ( ) 函式  
        ISEXCLUSIVE ( ) 函式  
    :::column-end:::
    :::column:::
        ISLEADBYTE ( ) 函式  
        ISLOWER ( ) 函式  
        ISNull ( ) 函式  
        ISREADONLY ( ) 函式  
        ISUPPER ( ) 函式  
    :::column-end:::
:::row-end:::

## <a name="k"></a>K  

:::row:::
    :::column:::
        KEY ( ) 函式
    :::column-end:::
    :::column:::
        KEYMATCH ( ) 函式
    :::column-end:::
:::row-end:::

## <a name="l"></a>L  

:::row:::
    :::column:::
         ( ) 函式  
        LEFTC ( ) 函式  
        LEN ( ) 函數  
        LENC ( ) 函式  
        例如 ( ) 函式  
        LIKEC ( ) 函式  
    :::column-end:::
    :::column:::
        本機命令  
        找出命令  
        鎖定 ( ) 函數  
        LOG ( ) 函數  
        LOG10 ( ) 函式  
        查閱 ( ) 函數  
    :::column-end:::
    :::column:::
        較低的 ( ) 函數  
        LPARAMETERS 命令  
        LTRIM ( ) 函式  
        LUPDATE ( ) 函式  
    :::column-end:::
:::row-end:::

## <a name="m"></a>M  

:::row:::
    :::column:::
        最大 ( ) 函數  
        MDX ( ) 函數  
        MDY ( ) 函式  
        MEMLINES ( ) 函式  
    :::column-end:::
    :::column:::
        MESSAGE ( ) 函式  
        MIN ( ) 函數  
        ) 函數 ( 分鐘  
        _MLINE 系統記憶體變數  
    :::column-end:::
    :::column:::
        MLINE ( ) 函式  
        MOD ( ) 函數  
        月 ( ) 函式  
        MTON ( ) 函式  
    :::column-end:::
:::row-end:::

## <a name="n"></a>N  

:::row:::
    :::column:::
        NDX ( ) 函式  
        標準化 ( ) 函式  
    :::column-end:::
    :::column:::
        NOT 運算子  
        注意命令  
    :::column-end:::
    :::column:::
        NTOM ( ) 函式  
        NVL ( ) 函式  
    :::column-end:::
:::row-end:::

## <a name="o"></a>O  

:::row:::
    :::column:::
         ( ) 函式時發生  
        OLDVAL ( ) 函式  
        ON ( ) 函數  
    :::column-end:::
    :::column:::
        ON ERROR 命令  
        ON KEY 命令  
        開啟資料庫命令  
    :::column-end:::
    :::column:::
        OR 運算子  
        順序 ( ) 函數  
        OS ( ) 函式  
    :::column-end:::
:::row-end:::

## <a name="p"></a>P  

:::row:::
    :::column:::
        PACK 命令  
        PADL ( ) &#124; PADR ( ) &#124; PADC ( ) 函數  
        PARAMETERS 命令  
         ( ) 函式的參數  
        付款 ( ) 函式  
    :::column-end:::
    :::column:::
        PI ( ) 函式  
        主要 ( ) 函式  
        PRI加值稅E 命令  
        PROCEDURE 命令  
        程式 ( ) 函式  
    :::column-end:::
    :::column:::
        適當的 ( ) 函數  
        PUBLIC 命令  
        PV ( ) 函數  
    :::column-end:::
:::row-end:::

## <a name="r"></a>R  

:::row:::
    :::column:::
        RAND ( ) 函數  
        RAT ( ) 函數  
        RATC ( ) 函式  
        RATLINE ( ) 函式  
        召回命令  
        RECCOUNT ( ) 函式  
        RECNO ( ) 函式  
        RECSIZE ( ) 函式  
    :::column-end:::
    :::column:::
        區域命令  
         ( ) 函式的關聯  
        移除資料表命令  
        REPLACE 命令  
        取代為數組命令  
        複寫 ( ) 函數  
        重試命令  
        RETURN 命令  
    :::column-end:::
    :::column:::
        RIGHT ( ) 函數  
        RIGHTC ( ) 函式  
        RLOCK ( ) 函式  
        ROLLBACK 命令  
        ROUND ( ) 函式  
        RTOD ( ) 函式  
        RTRIM ( ) 函式  
    :::column-end:::
:::row-end:::

## <a name="s"></a>S  

:::row:::
    :::column:::
        掃描。。。ENDSCAN 命令  
        散佈命令  
        SEC ( ) 函式  
         ( ) 函式的秒數  
        搜尋命令  
        搜尋 ( ) 函式  
        選取命令  
        選取 ( ) 函數  
        SELECT-SQL 命令  
        設定 ( ) 函數  
        SET BLOCKSIZE 命令  
        設定執行命令  
        設定世紀命令  
        SET COLLATE 命令  
        設定資料庫命令  
        設定日期命令  
        設定預設命令  
        SET DELETED 命令  
        SET EXACT 命令  
        SET EXCLUSIVE 命令  
        SET FDOW 命令  
    :::column-end:::
    :::column:::
        設定欄位命令  
        設定篩選命令  
        設定 FIXED 命令  
        SET FULLPATH 命令  
        SET FWEEK 命令  
        設定時數命令  
        設定索引命令  
        設定鎖定命令  
        SET MULTILOCKS 命令  
        設定 NEAR 命令  
        SET NOCPTRANS 命令  
        設定通知命令  
        SET NULL 命令  
        設定 OPTIMIZE 命令  
        設定順序命令  
        SET PATH 命令  
        SET PROCEDURE 命令  
        設定關聯性命令  
        設定關聯性命令  
        SET REPROCESS 命令  
        SET SKIP 命令  
    :::column-end:::
    :::column:::
        SET UDFPARMS 命令  
        SET UNIQUE 命令  
        設定 VOLUME 命令  
        SETFLDSTATE ( ) 函式  
        簽署 ( ) 函式  
         ( ) 函數的 SIN  
        SKIP 命令  
        SORT 命令  
         ( ) 函式的空間  
        SQRT ( ) 函式  
        STORE 命令  
        STR ( ) 函數  
        STRCONV ( ) 函式  
        STRTRAN ( ) 函式  
         ( ) 函式的內容  
        STUFFC ( ) 函式  
        SUBSTR ( ) 函式  
        SUBSTRC ( ) 函式  
        SUM 命令  
        SYS (2011) 函數  
    :::column-end:::
:::row-end:::

## <a name="t"></a>T  

:::row:::
    :::column:::
        TABLEREVERT ( ) 函式  
        TABLEUPDATE ( ) 函式  
        標記 ( ) 函式  
        TAGCOUNT ( ) 函式  
        TAGNO ( ) 函式  
        _TALLY 系統記憶體變數  
    :::column-end:::
    :::column:::
        TAN ( ) 函數  
        目標 ( ) 函式  
        TIME ( ) 函數  
        TOTAL 命令  
        _TRIGGERLEVEL 系統記憶體變數  
        TRIM ( ) 函數  
    :::column-end:::
    :::column:::
        TTOC ( ) 函式  
        TTOD ( ) 函式  
        TXNLEVEL ( ) 函式  
        輸入 ( ) 函數  
    :::column-end:::
:::row-end:::

## <a name="u"></a>U  

:::row:::
    :::column:::
        唯一 ( ) 函式  
        UNLOCK 命令  
        UPDATE 命令  
    :::column-end:::
    :::column:::
        UPDATE - SQL 命令  
        ) 函數的上層 (  
        使用命令  
    :::column-end:::
    :::column:::
        使用 ( ) 函式  
    :::column-end:::
:::row-end:::

## <a name="v"></a>V  

:::row:::
    :::column:::
        VAL ( ) 函數
    :::column-end:::
    :::column:::
        版本 ( ) 函式
    :::column-end:::
:::row-end:::

## <a name="w"></a>W  

 ( ) 函式的周

## <a name="y"></a>Y  

YEAR ( ) 函數

## <a name="z"></a>Z  

ZAP 命令
