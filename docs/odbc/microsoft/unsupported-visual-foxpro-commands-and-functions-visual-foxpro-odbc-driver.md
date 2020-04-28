---
title: 不支援的 Visual FoxPro 命令和函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], commands and functions
- functions [ODBC], Visual FoxPro
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro commands and functions
- FoxPro ODBC driver
ms.assetid: afdb6b7e-738d-42ca-8053-67ae50873ca6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e5b8ed06ad9f996d644df0dfb99d15adcff86bc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307649"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>不支援的 Visual FoxPro 命令和函式 (Visual FoxPro ODBC Driver)
下表列出 Visual FoxPro ODBC 驅動程式不支援的 FoxPro 命令和函式，但 Microsoft® Visual FoxPro®支援此功能。  
  
 如果您的應用程式與規則、觸發程式、預設值或預存程式呼叫這些 Visual FoxPro 命令或函式的資料互動，驅動程式可能會產生錯誤。  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>不支援的 Visual FoxPro 命令和函式  
  
||||  
|-|-|-|  
|#DEFINE ... #UNDEF|#IF ... #ENDIF 預處理器指示詞|#IFDEF &#124; #IFNDEF|  
|#INCLUDE 預處理器指示詞|：：範圍解析運算子|! 命令（請參閱 RUN &#124;！ 命令|  
|? &#124;？ Command|??? Command|\ &#124; \\\ 命令|  
|@ ...BOX 命令|@ ...類別命令|@ ...CLEAR 命令|  
|@ ...編輯-編輯方塊命令|@ ...FILL 命令|@ ...獲取|  
|@ ...功能表命令|@ ...提示命令|@ ...假設命令|  
|@ ...SCROLL 命令|@ ...TO 命令||  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ACCEPT 命令|ACLASS.INTERFACE （）函數|[啟動] 功能表命令|  
|啟動快捷方式命令|啟用螢幕命令|[啟動視窗] 命令|  
|ActivateCell 方法|新增類別命令|ADIR （）函數|  
|AFONT （）函數|AINSTANCE （）函數|_ALIGNMENT 系統記憶體變數|  
|AMEMBERS （）函數|ANSITOOEM （）函數|APRINTERS （）函數|  
|ASELOBJ （）函數|協助命令||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|BAR （）函數|BARCOUNT （）函數|BARPROMPT （）函數|  
|_BEAUTIFY 系統記憶體變數|_BOX 系統記憶體變數|流覽命令|  
|_BROWSER 系統記憶體變數|組建應用程式命令|BUILD EXE 命令|  
|組建專案命令|_BUILDER 系統記憶體變數||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|_CALCVALUE 系統記憶體變數|_CLIPTEXT 系統記憶體變數|_CONVERTER 系統記憶體變數|  
|_CUROBJ 系統記憶體變數|呼叫命令|取消命令|  
|CAPSLOCK （）函數|CD 命令|變更命令|  
|CHDIR 命令|CHRSAW （）函數|關閉備忘錄命令|  
|CNTBAR （）函數|CNTPAD （）函數|COL （）函數|  
|COMPILE 命令|COMPILE 資料庫命令|編譯表單命令|  
|COMPOBJ （）函數|容器物件|Control 物件|  
|複製檔案命令|複製備忘命令|建立類別命令|  
|建立 CLASSLIB 命令|建立 COLOR SET 命令|建立命令|  
|建立連接命令|建立資料庫命令|建立表單命令|  
|從命令建立|建立標籤命令|建立功能表命令|  
|建立專案命令|建立查詢命令|建立報表命令|  
|建立螢幕命令|建立 SQL VIEW 命令|建立觸發程式命令|  
|CREATE VIEW 命令|CREATEOBJECT （）函數|CURDIR （）函數|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|_DBLCLICK 系統記憶體變數|_DIARYDATE 系統記憶體變數|DBSETPROP （）函數|  
|DDE 函式|停用功能表命令|停用快顯視窗命令|  
|停用視窗命令|DECLARE-DLL 命令|DECLARE 命令|  
|定義橫條命令|定義 BOX 命令|定義類別命令|  
|定義功能表命令|定義 PAD 命令|定義 POPUP 命令|  
|定義視窗命令|刪除連接命令|刪除資料庫命令|  
|DELETE FILE 命令|DELETE 觸發程式命令|刪除 VIEW 命令|  
|DIR 命令|DIRECTORY 命令|顯示命令|  
|顯示連接命令|顯示資料庫命令|顯示 DLL 命令|  
|顯示檔案命令|顯示記憶體命令|顯示物件命令|  
|顯示程式命令|顯示狀態命令|顯示結構命令|  
|顯示資料表命令|顯示 VIEWS 命令|執行表單命令|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|編輯命令|ERROR 命令||  
|清除命令|外部命令|匯出命令|  
|退出命令|退出頁面命令||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|_FOXDOC 系統記憶體變數|_FOXGRAPH 系統記憶體變數|FEOF （）函數|  
|FCLOSE （）函數|FCREATE （）函數|FGETS （）函數|  
|FERROR （）函數|FFLUSH （）函數|FKLABEL （）函數|  
|檔案管理工具命令|尋找命令|FOPEN （）函數|  
|FKMAX （）函數|FONTMETRIC （）函數|FSEEK （）函數|  
|FPUTS （）函數|FREAD （）函數||  
|FWRITE （）函數|FCHSIZE （）函數||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|_GENGRAPH 系統記憶體變數|_GENMENU 系統記憶體變數|_GENPD 系統記憶體變數|  
|_GENSCRN 系統記憶體變數|_GENXTAB 系統記憶體變數|FOO.GETBAR （）函數|  
|GETCOLOR （）函數|GETDIR （）函數|GETEXPR 命令|  
|GETFILE （）函數|IVSFONTANDCOLORSTORAGE.GETFONT （）函數|GETOBJECT （）函數|  
|GETPAD （）函數|GETPICT （）函數|GETPRINTER （）函數|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|HELP 命令|隱藏功能表命令|隱藏 POPUP 命令|  
|隱藏視窗命令|HOME （）函數||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IMESTATUS （）函數|匯入命令|輸入命令|  
|命令上的索引|INKEY （）函數|ISCOLOR （）函數|  
|插入命令|INSMODE （）函數||  
|ISMOUSE （）函數|_INDENT 系統記憶體變數||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|聯結命令|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|鍵盤命令|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|_LMARGIN 系統記憶體變數|標籤命令|IF GRAPHICSWINDOW.LASTKEY （）函數|  
|LINENO （）函數|列出命令|列出連接命令|  
|載入命令|LOCFILE 中（）函數||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|MCOL （）函數|MD 命令|命令的功能表|  
|MEMORY （）函數|功能表命令|MKDIR 命令|  
|MENU （）函數|MESSAGEBOX （）函數|修改連接命令|  
|MODIFY CLASS 命令|MODIFY 命令命令|修改表單命令|  
|修改資料庫命令|MODIFY FILE 命令|修改備忘錄命令|  
|修改一般命令|修改標籤命令|修改專案命令|  
|修改功能表命令|MODIFY PROCEDURE 命令|修改螢幕命令|  
|修改查詢命令|修改報告命令|修改視窗命令|  
|MODIFY STRUCTURE 命令|修改 VIEW 命令|移動視窗命令|  
|滑鼠命令|MOVE POPUP 命令|MROW （）函數|  
|MRKBAR （）函數|MRKPAD （）函數||  
|MWINDOW （）函數|MDOWN （）函數||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NUMLOCK （）函數|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|OBJNUM （）函數|OBJTOCLIENT （）函數|ON BAR 命令|  
|OEMTOANSI （）函數|ON APLABOUT 命令|在結束功能表命令上|  
|ON ESCAPE 命令|ON EXIT BAR 命令|ON KEY = 命令|  
|ON EXIT PAD 命令|ON EXIT POPUP 命令|ON PAD 命令|  
|ON KEY LABEL 命令|ON MACHELP 命令|ON 選取列命令|  
|在頁面命令上|ON READERROR 命令|ON 選取快顯視窗命令|  
|在選取功能表命令上|ON 選取範圍面板命令||  
|ON SHUTDOWN 命令|OBJVAR （）函數||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|_PADVANCE 系統記憶體變數|_PAGENO 系統記憶體變數|_PBPAGE 系統記憶體變數|  
|_PCOLNO 系統記憶體變數|_PCOPIES 系統記憶體變數|_PDRIVER 系統記憶體變數|  
|_PDSETUP 系統記憶體變數|_PECODE 系統記憶體變數|_PEJECT 系統記憶體變數|  
|_PEPAGE 系統記憶體變數|_PLENGTH 系統記憶體變數|_PLINENO 系統記憶體變數|  
|_PLOFFSET 系統記憶體變數|_PPITCH 系統記憶體變數|_PQUALITY 系統記憶體變數|  
|_PRETEXT 系統記憶體變數|_PSCODE 系統記憶體變數|_PSPACING 系統記憶體變數|  
|_PWAIT 系統記憶體變數|PACK 資料庫命令|PAD （）函數|  
|PCOL （）函數|PEMSTATUS （）函數|PLAY 巨集命令|  
|POP 按鍵命令|快顯功能表命令|快顯視窗命令|  
|POPUP （）函數|PRINTJOB ...ENDPRINTJOB 命令|PRINTSTATUS （）函數|  
|PRMBAR （）函數|PRMPAD （）函數|PROMPT （）函數|  
|PROW （）函數|PRTINFO （）函數|PUSH KEY 命令|  
|[推播功能表] 命令|PUSH POPUP 命令|PUTFILE （）函數|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|QUIT 命令|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|_RMARGIN 系統記憶體變數|RD 命令|READKEY （）函數|  
|讀取命令|讀取功能表命令|發行條命令|  
|REFRESH （）函數|重新編制索引命令|發行程式庫命令|  
|RELEASE CLASSLIB 命令|RELEASE 命令|RELEASE PAD 命令|  
|發行功能表命令|RELEASE MODULE 命令|發行 WINDOWS 命令|  
|釋放快顯視窗命令|RELEASE PROCEDURE 命令|RENAME 命令|  
|REMOVE CLASS 命令|RENAME 類別命令|重新命名 VIEW 命令|  
|重新命名連接命令|重新命名資料表命令|從命令還原|  
|報表命令|REQUERY （）函數|還原視窗命令|  
|還原巨集命令|RESTORE SCREEN 命令|RGBSCHEME （）函數|  
|繼續命令|RGB （）函數|執行 &#124;！ Command|  
|RMDIR 命令|ROW （）函數||  
|RUNSCRIPT 命令|RDLEVEL （）函數||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|儲存巨集命令|儲存螢幕命令|儲存至命令|  
|儲存 WINDOWS 命令|配置（）函數|SCOLS （）函數|  
|SCROLL 命令|_SCREEN 系統記憶體變數|SET 命令|  
|設定替代命令|SET ANSI 命令|SET APLABOUT 命令|  
|設定自動儲存命令|設定鐘命令|設定閃爍命令|  
|設定框線命令|SET BRSTATUS 命令|SET CLASSLIB 命令|  
|SET CLEAR 命令|設定時鐘命令|設定命令的色彩|  
|設定配置命令的色彩|SET COLOR SET 命令|將色彩設定為命令|  
|設定相容的命令|設定 CONFIRM 命令|設定主控台命令|  
|設定 CPCOMPILE|設定 CPDIALOG|SET CURRENCY 命令|  
|SET CURSOR 命令|SET DATASESSION 命令|設定 DEBUG 命令|  
|設定小數命令|SET 分隔符號命令|設定開發命令|  
|設定裝置命令|設定顯示命令|SET DOHISTORY 命令|  
|設定 ECHO 命令|設定 ESCAPE 命令|設定格式命令|  
|設定函式命令|設定標題命令|SET HELP 命令|  
|SET HELPFILTER 命令|設定濃度命令|SET KEY 命令|  
|SET KEYCOMP 命令|SET LOGERRORS 命令|SET MACDESKTOP 命令|  
|SET MACHELP 命令|SET MACKEY 命令|設定 MARGIN 命令|  
|設定命令的標記|將標記設定為命令|SET MEMOWIDTH 命令|  
|設定訊息命令|設定滑鼠命令|SET 里程表讀數命令|  
|SET OLEOBJECT 命令|設定調色板命令|SET PDSETUP 命令|  
|SET POINT 命令|設定印表機命令|SET READBORDER 命令|  
|設定 REFRESH 命令|設定資源命令|設定安全性命令|  
|設定計分板命令|設定秒數命令|SET SEPARATOR 命令|  
|設定 SHADOWS 命令|設定略過命令|SET SPACE 命令|  
|設定狀態命令|設定狀態列命令|SET STEP 命令|  
|設定粘滯命令|SET SYSFORMATS 命令|SET SYSMENU 命令|  
|設定交談命令|SET TEXTMERGE 命令|SET TEXTMERGE 分隔符號命令|  
|設定主題命令|設定主題 ID 命令|SET TRBETWEEN 命令|  
|SET 自動提示命令|SET VIEW 命令|備忘命令的設定視窗|  
|SET XCMDFILE 命令|_SHELL 系統記憶體變數|顯示 GET 命令|  
|SHOW 取得命令|顯示功能表命令|顯示物件命令|  
|SHOW POPUP 命令|顯示視窗命令|SIZE POPUP 命令|  
|大小視窗命令|SKPBAR （）函數|SKPPAD （）函數|  
|SOUNDEX （）函數|_SPELLCHK 系統記憶體變數|SQL 函數|  
|SROWS （）函數|_STARTUP 系統記憶體變數|暫止命令|  
|Sys （）函數（SYS （2011）除外）|SYSMETRIC （）函數||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TABS 系統記憶體變數|文字 .。。ENDTEXT 命令|TXTWIDTH （）函數|  
|TRANSFORM （）函數|_TRANSPORT 系統記憶體變數||  
|類型命令|_THROTTLE 系統記憶體變數||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|UPDATED （）函數|使用命令||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|驗證資料庫命令|VARREAD （）函數|VERSION （）函數|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|_WINDOWS 系統記憶體變數|_WIZARD 系統記憶體變數|WCHILD （）函數|  
|WAIT 命令|WBORDER （）函數|WFONT （）函數|  
|WCOLS （）函數|WEXIST （）函數|WLROW （）函數|  
|使用 .。。ENDWITH 命令|WLAST （）函數|WONTOP （）函數|  
|WMAXIMUM （）函數|WLCOL （）函數|WREAD （）函數|  
|WOUTPUT （）函數|WMINIMUM （）函數|WVISIBLE （）函數|  
|WPARENT （）函數|WTITLE （）函數||  
|WROWS （）函數|_WRAP 系統記憶體變數||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZOOM 視窗命令|||
