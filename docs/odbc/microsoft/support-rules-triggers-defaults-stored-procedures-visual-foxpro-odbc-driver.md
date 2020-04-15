---
title: 支援規則、觸發器、預設值和存儲過程 |微軟文件
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
ms.openlocfilehash: 2fcf8e7c80b2712313cba81199489dc7cb06dce0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301135"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>規則、觸發程序、預設值和預存程序支援 (Visual FoxPro ODBC Driver)
無法使用 Visual FoxPro ODBC 驅動程式創建 Visual FoxPro 規則、觸發器、預設值或儲存過程。 但是,應用程式可能會在插入、更新或刪除存儲在資料庫中的 Visual FoxPro 資料時與現有規則、觸發器、預設值或存儲過程進行交互。  
  
 下表列出了 Visual FoxPro ODBC 驅動程式支援的 Visual FoxPro 命令和函數,當命令或函數存在於規則、觸發器、預設值或儲存過程中時。  
  
 如果應用程式與規則、觸發器、預設值或儲存過程呼叫任何其他 Visual FoxPro 命令或函數的資料進行互動,則驅動程式將生成錯誤。 有關驅動程式不支援的命令和函數清單,請參閱[不支援的 Visual FoxPro 命令和函數](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md)清單。  
  
> [!TIP]  
>  如果要將條件代碼插入到確定驅動程式呼叫時要執行的命令的規則、觸發器或儲存過程中,可以使用**VERSION( )** 函數。 當驅動程式呼叫時 **,VERSION()** 函數傳回"視覺 FoxPro ODBC 驅動程式*\<版本>"。*  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>在規則、觸發器、預設值和儲存過程中支援視覺化 FoxPro 指令和函數  
  
||||  
|-|-|-|  
|$ 運算子|% 運算子|&命令|  
|&& 指挥部|• 命令|• 命令|  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ABS( ) 功能|ACOPY) 功能|新增表指令|  
|ADATABASES( )|ADBOBJECTS( )|AERROR 功能|  
|ADEL( ) 功能|AELEMENT) 功能|放大縮小字型功能 放大縮小字型功能|  
|AFIELDS( ) 功能|AINSS( ) 功能|ALTER TABLE - SQL 命令|  
|ALIAS) 功能|ALLTRIM( ) 功能|從 ARRAY 指令的附錄|  
|和管理員|APPEND 命令|APPEND MEMO 指令|  
|從命令中套用|APPEND 總司令部|ASCANS 功能|  
|放大縮小字型功能 放大縮小字型功能|ASC( ) 功能|放大縮小字型功能 放大縮小字型功能|  
|ASIN) 功能|ASORT) 功能|ATAN( ) 功能|  
|AT( ) 功能|AT_C( ) 功能|ATCLINE( ) 功能|  
|ATC( ) 功能|ATCC( ) 功能|AUSED) 功能|  
|ATline( ) 功能|ATN2( ) 功能||  
|平均命令|ACOS( ) 功能||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|BEGIN 交易命令|() 功能|BITNOT( ) 功能|  
|BITCLEAR( )|BITLSHIFT) 功能|BITSET) 功能|  
|BITOR( ) 功能|BITRSHIFT) 功能|BLANK 命令|  
|BITTEST( ) 功能|BITXOR( ) 功能||  
|BOF( ) 功能|BITand( ) 功能||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|計算命令|候選人( ) 功能|CHR( ) 職能|  
|CDX( ) 功能|天花板( ) 功能|關閉命令|  
|CHRTRAN( ) 功能|CHRTRANC( ) 功能|複製索引指令|  
|CMONTH) 功能|繼續命令|複製結構延伸命令|  
|複製程式指令|複製結構命令|複製到指令|  
|複製分頁命令|複製到 ARRAY 命令|CPCONVERT) 功能|  
|COS( ) 功能|COUNT 命令|CTOD( ) 功能|  
|CPCURRENTS( ) 功能|CPDBF( ) 功能|放大縮小字型功能 放大縮小字型功能|  
|CTOT( ) 功能|放大縮小字型功能 放大縮小字型功能||  
|曲線( ) 功能|CDOW( ) 功能||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|日期( ) 功能|日期時間( ) 功能|日( ) 功能|  
|DBC( ) 功能|DBF( ) 功能|DBGETPROP( )|  
|DBused( ) 功能|DELETE - SQL 命令|移除命令|  
|DELETE TAG 命令|刪除( ) 功能|遞減( ) 功能|  
|差異( ) 功能|維度命令|磁碟空間( ) 功能|  
|DMY( ) 功能|做案例...ENDCASE 命令|動作命令|  
|做, 而 ...ENDDO 命令|DOW( ) 功能|DTOC( ) 功能|  
|DTOR( ) 功能|DTOS( ) 功能|DTOT( ) 功能|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|放大縮小字型功能 放大縮小字型功能|評估( ) 功能|EXIT 命令|  
|錯誤( ) 功能|EXP( ) 功能||  
|結束交易命令|EOF( ) 功能||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|FCOUNT( ) 功能|FDATE) 功能|放大縮小字型功能 放大縮小字型功能|  
|檔案( ) 功能|過濾器( ) 功能|FLDLIST( ) 功能|  
|FLOCK( ) 功能|地板( ) 功能|FLUSH 命令|  
|對於 ...ENDFOR 指令|for( ) 功能|FOUND( ) 功能|  
|自由表命令|FSIZE( ) 功能|FTIME( ) 功能|  
|全路徑( ) 功能|職能命令|FV( ) 功能|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|GATHER 指令|放大縮小字型功能 放大縮小字型功能|GO/GOTO 指令|  
|GETFLDSTATE( )|GOmonth) 功能||  
|GETCP( ) 功能|GETENV( ) 功能||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|標題( ) 功能|小時( ) 功能|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE) 功能|如果。。。恩迪夫命令|IIF( ) 功能|  
|INDBC( ) 功能|INDEX 命令|INlist( ) 功能|  
|插入 SQL 指令|INT( ) 功能|ISALPHA( ) 功能|  
|ISBLANK( ) 功能|ISDigitS 功能|是排他性( )|  
|ISleadBY( )|ISLOWER( ) 功能|ISNULL( ) 功能|  
|ISREAD) 功能|ISupper( ) 功能||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|鍵( ) 功能|鍵符合( ) 功能||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|左( ) 功能|左撇子( ) 功能|(完) 功能|  
|LENC( ) 功能|喜歡) 功能|鎖定 ) 功能|  
|本地指令|定位命令|尋找( ) 功能|  
|紀錄( ) 功能|LOG10( ) 功能|LTRIM( ) 功能|  
|低() 功能|LPARAMETERS 命令||  
|放大縮小字型功能 放大縮小字型功能|LEN( ) 功能||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE系統記憶體變數|最大() 功能|MDX( ) 功能|  
|MDY( ) 功能|MEMLINES( ) 功能|訊息( ) 功能|  
|最小值 ) 功能|分鐘( ) 功能|MLINE( ) 功能|  
|MOD( ) 功能|月( ) 功能|MTONS ) 功能|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NDX( ) 功能|放大縮小字型功能 放大縮小字型功能|不是操作員|  
|註解命令|NTOM( ) 功能|NVL( ) 功能|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|發生( ) 功能|舊瓦爾( ) 功能|上錯誤命令|  
|在關鍵命令|開啟( ) 功能|開啟資料庫命令|  
|或管理員|訂單( ) 功能|作業系統( ) 功能|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|PACK 命令|參數( ) 功能|付款( )|  
|參數命令|初級功能|私人命令|  
|PI( ) 功能|程式( ) 功能|正( ) 功能|  
|程式命令|PV( ) 功能||  
|公開命令|PADL( ) &#124; PADR( ) &#124; PADC ( ) 功能||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|蘭德( ) 功能|RAT( ) 功能|RATC( ) 功能|  
|RATLINE( ) 功能|RECALL 命令|(完) 功能|  
|RECNO( ) 功能|放大縮小字型功能 放大縮小字型功能|區域司令部|  
|關聯( ) 功能|移除 TABLE 命令|取代命令|  
|從 ARRAY 命令取代|複製( ) 功能|RETRY 命令|  
|返回命令|右) 功能|右C( ) 功能|  
|RLOCK( ) 功能|捲軸|ROUND( ) 功能|  
|RTOD( ) 功能|RTRIM( ) 功能||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|掃描。。。ENDSCAN 命令|分散命令|SEC( ) 功能|  
|放大縮小字型功能 放大縮小字型功能|SEEK 指令|服務( ) 功能|  
|選擇指令|選擇( ) 功能|SELECT-SQL 指令|  
|SET BLOCKSIZE 命令|SET CARRY 命令|設定世紀指令|  
|SET COLLATE 命令|設定資料庫命令|SET 日期命令|  
|設定預設指令|SET DELETED 命令|SET EXACT 命令|  
|SET EXCLUSIVE 命令|SET FDOW 命令|SET FIELDS 命令|  
|設定篩選器指令|設定固定命令|設定全PATH命令|  
|SET FWEEK 命令|SETHOURS 命令|SET INDEX 命令|  
|設定鎖定命令|設定多鎖命令|設定近指令|  
|設定 NOCPTRANS 命令|設定通知命令|SET NULL 命令|  
|設定最佳化指令|SET ORDER 命令|SET PATH 命令|  
|設定程式指令|設定關聯指令|設定關聯關閉命令|  
|SET REPROCESS 命令|SET SKIP 命令|SET UDFPARMS 命令|  
|SET UNIQUE 命令|SET VOLUME 命令|設定) 功能|  
|SETFLDSTATE( )|符號 ( ) 功能|SINS ) 功能|  
|SKIP 命令|SORT 命令|空白( ) 功能|  
|SQRT( ) 功能|儲存命令|STR( ) 功能|  
|STRCONV( ) 功能|放大縮小字型功能 放大縮小字型功能|STUFF( ) 功能|  
|STUFFC( ) 功能|SUBSTR( ) 功能|SUBSTRC( ) 功能|  
|SUM 命令|SYS(2011)功能||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY系統記憶體變數|_TRIGGERLEVEL系統記憶體變數|標籤計數( )|  
|更新( ) 功能|標記( ) 功能|目標( ) 功能|  
|TAGNO( ) 功能|TAN( ) 功能|修剪( ) 功能|  
|時間( ) 功能|總命令|TXNLEVEL( )|  
|TTOC( ) 功能|TTOD( ) 功能||  
|型態( ) 功能|表還原( ) 功能||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|唯一功能|UNLOCK 命令|使用指令|  
|更新命令|上部( ) 功能||  
|已用 ( ) 功能|UPDATE - SQL 命令||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL( ) 功能|版本( ) 功能||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|週( ) 功能|||  
  
## <a name="y"></a>Y  
  
||||  
|-|-|-|  
|年( ) 功能|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZAP 命令|||
