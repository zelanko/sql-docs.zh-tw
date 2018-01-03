---
title: "Visual FoxPro 命令和函數不支援 |Microsoft 文件"
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
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], commands and functions
- functions [ODBC], Visual FoxPro
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro commands and functions
- FoxPro ODBC driver
ms.assetid: afdb6b7e-738d-42ca-8053-67ae50873ca6
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 85d11ebb5fd4245a7c6b5cf7c277e45d8df90011
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>不支援 Visual FoxPro 命令與函式 （Visual FoxPro ODBC 驅動程式）
下表列出 FoxPro 命令與不支援 Visual FoxPro ODBC 驅動程式，但 Microsoft® Visual FoxPro® 所支援的函式。  
  
 如果您的應用程式會與資料互動，其規則、 觸發程序、 預設值，或預存程序呼叫這些 Visual FoxPro 命令或函式，此驅動程式可能會產生錯誤。  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>不支援 Visual FoxPro 命令和函數  
  
||||  
|-|-|-|  
|#DEFINE...#UNDEF|...#IF #ENDIF 前置處理器指示詞|#IFDEF &#124;#IFNDEF|  
|#INCLUDE 前置處理器指示詞|:: 範圍解析運算子|! 命令 （請參閱執行 &#124; ！ 命令中）|  
|? &#124; ?? 命令|??? 命令|\ &#124;\\\ 命令|  
|@ ...方塊命令|@ ...命令類別|@ ...清除命令|  
|@ ...編輯-編輯方塊命令|@ ...填滿命令|@ ...GET|  
|@ ...功能表命令|@ ...提示字元命令|@ ...說出命令|  
|@ ...捲動命令|@ ...命令||  
  
## <a name="a"></a>只有在次要複本設定成手動容錯移轉模式，而且至少一個次要複本目前與主要複本 SYNCHRONIZED 時，  
  
||||  
|-|-|-|  
|接受命令|ACLASS （） 函式|啟用功能表命令|  
|啟用快顯功能表命令|啟動螢幕的命令|啟動 [視窗] 命令|  
|ActivateCell 方法|新增類別 命令|ADIR （） 函式|  
|AFONT （） 函式|AINSTANCE （） 函式|_ALIGNMENT 系統記憶體變數|  
|AMEMBERS （） 函式|ANSITOOEM （） 函式|APRINTERS （） 函式|  
|ASELOBJ （） 函式|協助命令||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|列 （） 函式|BARCOUNT （） 函式|BARPROMPT （） 函式|  
|_BEAUTIFY 系統記憶體變數|_BOX 系統記憶體變數|瀏覽命令|  
|_BROWSER 系統記憶體變數|建置應用程式的命令|建置 EXE 命令|  
|建置專案命令|_BUILDER 系統記憶體變數||  
  
## <a name="c"></a>c  
  
||||  
|-|-|-|  
|_CALCVALUE 系統記憶體變數|_CLIPTEXT 系統記憶體變數|_CONVERTER 系統記憶體變數|  
|_CUROBJ 系統記憶體變數|呼叫命令|取消命令|  
|CAPSLOCK （） 函式|CD 命令|變更命令|  
|CHDIR 命令|CHRSAW （） 函式|關閉備忘命令|  
|CNTBAR （） 函式|CNTPAD （） 函式|資料行 （） 函式|  
|編譯命令|編譯資料庫命令|編譯表單命令|  
|COMPOBJ （） 函式|容器物件|控制項物件|  
|複製檔案命令|複製備忘 命令|建立類別 命令|  
|建立類別庫命令|建立色彩 SET 命令|建立命令|  
|建立連線的命令|建立資料庫命令|建立表單命令|  
|建立命令|建立標籤命令|建立功能表命令|  
|建立專案命令|建立查詢命令|建立報表的命令|  
|建立螢幕的命令|建立檢視的 SQL 命令|建立觸發程序命令|  
|建立檢視命令|CREATEOBJECT （） 函式|會將 CURDIR （） 函式|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|_DBLCLICK 系統記憶體變數|_DIARYDATE 系統記憶體變數|DBSETPROP （） 函式|  
|DDE 函式|停用功能表命令|停用快顯功能表命令|  
|停用視窗命令|宣告-DLL 命令|宣告命令|  
|定義命令列|定義命令方塊|定義類別命令|  
|定義功能表命令|定義板命令|定義快顯功能表命令|  
|定義視窗 命令|刪除連接命令|刪除資料庫命令|  
|刪除檔案命令|刪除觸發程序命令|刪除檢視命令|  
|DIR 命令|目錄命令|顯示命令|  
|顯示 [連線] 命令|顯示資料庫命令|顯示 DLL 命令|  
|顯示檔案命令|顯示記憶體命令|顯示物件命令|  
|顯示程序命令|顯示 [狀態] 命令|顯示結構命令|  
|顯示資料表 命令|顯示檢視命令|表單命令|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|編輯命令|錯誤的命令||  
|清除命令|外部命令|匯出命令|  
|退出命令|退出頁面命令||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|_FOXDOC 系統記憶體變數|_FOXGRAPH 系統記憶體變數|FEOF （） 函式|  
|FCLOSE （） 函式|FCREATE （） 函式|FGETS （） 函式|  
|FERROR （） 函式|FFLUSH （） 函式|FKLABEL （） 函式|  
|檔案命令|尋找命令|FOPEN （） 函式|  
|FKMAX （） 函式|FONTMETRIC （） 函式|FSEEK （） 函式|  
|FPUTS （） 函式|FREAD （） 函式||  
|FWRITE （） 函式|FCHSIZE （） 函式||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|_GENGRAPH 系統記憶體變數|_GENMENU 系統記憶體變數|_GENPD 系統記憶體變數|  
|_GENSCRN 系統記憶體變數|_GENXTAB 系統記憶體變數|GETBAR （） 函式|  
|GETCOLOR （） 函式|GETDIR （） 函式|GETEXPR 命令|  
|GETFILE （） 函式|GETFONT （） 函式|GETOBJECT （） 函式|  
|GETPAD （） 函式|GETPICT （） 函式|GETPRINTER （） 函式|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|[說明] 命令|隱藏功能表命令|隱藏快顯功能表命令|  
|隱藏視窗命令|首頁 （） 函式||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IMESTATUS （） 函式|匯入命令|輸入的命令|  
|命令上的索引|INKEY （） 函式|ISCOLOR （） 函式|  
|插入命令|INSMODE （） 函式||  
|ISMOUSE （） 函式|_INDENT 系統記憶體變數||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|加入命令|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|鍵盤命令|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|_LMARGIN 系統記憶體變數|標籤命令|LASTKEY （） 函式|  
|LINENO （） 函式|清單命令|列出連接命令|  
|載入命令|LOCFILE （） 函式||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|MCOL （） 函式|MD 命令|功能表命令|  
|記憶體 （） 函式|功能表命令|MKDIR 命令|  
|功能表 （） 函式|MESSAGEBOX （） 函式|修改連接命令|  
|修改類別命令|修改命令|修改表單命令|  
|修改資料庫命令|修改檔案命令|修改備忘命令|  
|修改一般命令|修改 [標籤] 命令|修改專案命令|  
|修改功能表命令|修改程序命令|修改螢幕的命令|  
|修改查詢命令|修改報表命令|修改 [視窗] 命令|  
|修改結構命令|修改檢視 命令|移動視窗命令|  
|滑鼠命令|移動快顯功能表命令|MROW （） 函式|  
|MRKBAR （） 函式|MRKPAD （） 函式||  
|MWINDOW （） 函式|MDOWN （） 函式||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NUMLOCK （） 函式|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|OBJNUM （） 函式|OBJTOCLIENT （） 函式|在命令列|  
|OEMTOANSI （） 函式|APLABOUT 命令|ON EXIT 功能表命令|  
|逸出命令|在結束工具列命令|機碼 = 命令|  
|ON EXIT 板命令|ON EXIT 快顯功能表命令|ON 板命令|  
|在索引鍵的標籤命令|MACHELP 命令|在選取項目列命令|  
|在頁面上的命令|READERROR 命令|選取快顯功能表命令|  
|選取功能表命令|在選取項目板命令||  
|在 [關機] 命令|OBJVAR （） 函式||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|_PADVANCE 系統記憶體變數|_PAGENO 系統記憶體變數|_PBPAGE 系統記憶體變數|  
|_PCOLNO 系統記憶體變數|_PCOPIES 系統記憶體變數|_PDRIVER 系統記憶體變數|  
|_PDSETUP 系統記憶體變數|_PECODE 系統記憶體變數|_PEJECT 系統記憶體變數|  
|_PEPAGE 系統記憶體變數|_PLENGTH 系統記憶體變數|_PLINENO 系統記憶體變數|  
|_PLOFFSET 系統記憶體變數|_PPITCH 系統記憶體變數|_PQUALITY 系統記憶體變數|  
|_PRETEXT 系統記憶體變數|_PSCODE 系統記憶體變數|_PSPACING 系統記憶體變數|  
|_PWAIT 系統記憶體變數|組件 DATABASE 命令|填補 （） 函式|  
|PCOL （） 函式|PEMSTATUS （） 函式|播放巨集命令|  
|快顯按鍵命令|快顯功能表命令|POP 快顯功能表命令|  
|快顯視窗 （） 函式|列印工作...ENDPRINTJOB 命令|PRINTSTATUS （） 函式|  
|PRMBAR （） 函式|PRMPAD （） 函式|提示 > （） 函式|  
|PROW （） 函式|PRTINFO （） 函式|推入快速鍵命令|  
|推入功能表命令|推入快顯功能表命令|PUTFILE （） 函式|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|QUIT 命令|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|_RMARGIN 系統記憶體變數|RD 命令|READKEY （） 函式|  
|讀取命令|讀取功能表命令|版本列命令|  
|REFRESH() 函式|重新索引命令|發行文件庫命令|  
|發行類別庫命令|發行命令|發行板命令|  
|發行功能表命令|發行模組命令|發行 WINDOWS 命令|  
|發行快顯命令|版本的程序命令|重新命名命令|  
|移除類別 命令|重新命名類別命令|重新命名檢視命令|  
|重新命名連線命令|重新命名的資料表 命令|還原命令|  
|報表命令|重新查詢 > （） 函式|還原 [視窗] 命令|  
|RESTORE 命令巨集|還原 [螢幕] 命令|RGBSCHEME （） 函式|  
|RESUME 命令|RGB （） 函式|執行 &#124; ！ 命令|  
|RMDIR 命令|資料列 （） 函式||  
|RUNSCRIPT 命令|RDLEVEL （） 函式||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|儲存命令巨集|儲存螢幕 命令|將儲存至命令|  
|儲存 WINDOWS 命令|配置 > （） 函式|SCOLS （） 函式|  
|捲動命令|_SCREEN 系統記憶體變數|SET 命令|  
|SET 替代命令|SET ANSI 命令|SET APLABOUT 命令|  
|設定自動儲存命令|SET 鈴鐺命令|SET 閃爍命令|  
|SET 框線命令|SET BRSTATUS 命令|SET 類別庫命令|  
|SET 清除命令|SET 時鐘命令|設定色彩的命令|  
|設定色彩配置 命令的|設定色彩設定命令|設定色彩，到命令|  
|SET 相容命令|SET 確認命令|SET 主控台命令|  
|設定 CPCOMPILE|設定 CPDIALOG|SET 貨幣命令|  
|SET CURSOR 命令|SET 表格作業區命令|設定偵錯命令|  
|SET 小數命令|SET 分隔符號命令|SET 開發命令|  
|設定裝置命令|SET 顯示命令|SET DOHISTORY 命令|  
|SET ECHO 命令|SET 逸出命令|SET 格式命令|  
|SET 函式命令|SET 標題命令|設定 [說明] 命令|  
|SET HELPFILTER 命令|SET 濃度命令|設定機碼命令|  
|SET KEYCOMP 命令|SET LOGERRORS 命令|SET MACDESKTOP 命令|  
|SET MACHELP 命令|SET MACKEY 命令|SET 邊界命令|  
|設定標記的命令|設定標記成命令|SET MEMOWIDTH 命令|  
|SET 訊息命令|SET 滑鼠命令|SET 里程計命令|  
|SET OLEOBJECT 命令|SET 調色盤命令|SET PDSETUP 命令|  
|設定點命令|SET 印表機命令|SET READBORDER 命令|  
|設定重新整理命令|SET 資源命令|SET 安全命令|  
|SET 排行榜命令|SET 秒命令|SET 分隔符號命令|  
|SET 陰影命令|設定略過的命令|SET 空間命令|  
|設定 [狀態] 命令|設定狀態 列命令|設定逐步執行 命令|  
|SET 自黏命令|SET SYSFORMATS 命令|SET SYSMENU 命令|  
|SET TALK 命令|SET 文字合併命令|SET 文字合併分隔符號命令|  
|SET 主題命令|SET 主題識別碼命令|SET TRBETWEEN 命令|  
|SET TYPEAHEAD 命令|SET 檢視命令|設定視窗的備忘命令|  
|SET XCMDFILE 命令|_SHELL 系統記憶體變數|顯示 GET 命令|  
|顯示 [取得] 命令|顯示功能表命令|顯示物件命令|  
|顯示快顯功能表命令|顯示視窗 命令|大小快顯功能表命令|  
|大小 [視窗] 命令|SKPBAR （） 函式|SKPPAD （） 函式|  
|SOUNDEX （） 函式|_SPELLCHK 系統記憶體變數|SQL 函數|  
|SROWS （） 函式|_STARTUP 系統記憶體變數|暫停命令|  
|除了 SYS(2011) SYS() 函式|SYSMETRIC （） 函式||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TABS 系統記憶體變數|文字...ENDTEXT 命令|TXTWIDTH （） 函式|  
|轉換 （） 函式|_TRANSPORT 系統記憶體變數||  
|輸入命令|_THROTTLE 系統記憶體變數||  
  
## <a name="u"></a>u  
  
||||  
|-|-|-|  
|更新 （） 函式|使用命令||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|驗證資料庫命令|VARREAD （） 函式|版本 （） 函式|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Windows （_w） 系統記憶體變數|_WIZARD 系統記憶體變數|WCHILD （） 函式|  
|等候命令|WBORDER （） 函式|WFONT （） 函式|  
|WCOLS （） 函式|WEXIST （） 函式|WLROW （） 函式|  
|與...ENDWITH 命令|WLAST （） 函式|WONTOP （） 函式|  
|WMAXIMUM （） 函式|WLCOL （） 函式|WREAD （） 函式|  
|WOUTPUT （） 函式|WMINIMUM （） 函式|WVISIBLE （） 函式|  
|WPARENT （） 函式|WTITLE （） 函式||  
|WROWS （） 函式|_WRAP 系統記憶體變數||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|縮放視窗命令|||
