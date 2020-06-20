---
title: 使用查詢編輯器編輯 SQLCMD 指令碼
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], SQLCMD scripts
- SQLCMD scripts
- modifying scripts
- Query Editor [Database Engine], SQLCMD scripts
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: f77b866d-c330-47c9-9e74-0b8d8dff4b31
author: rothja
ms.author: jroth
ms.openlocfilehash: afcf38e662b152a5039043017624a46b214e263f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065762"
---
# <a name="edit-sqlcmd-scripts-with-query-editor"></a>使用查詢編輯器編輯 SQLCMD 指令碼
  您可以使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器，以 SQLCMD 指令碼撰寫和編輯查詢。 當您必須在相同的指令碼中處理 Windows 系統命令和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式時，就可以使用 SQLCMD 指令碼。  
  
## <a name="sqlcmd-mode"></a>SQLCMD 模式  
 若要使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器來撰寫或編輯 SQLCMD 指令碼，您必須啟用 SQLCMD 指令碼模式。 根據預設，查詢編輯器不會啟用 SQLCMD 模式。 您可以按一下工具列上的 **SQLCMD 模式**圖示，或從 [查詢] 功能表中選取 [SQLCMD 模式]啟用指令碼模式。  
  
> [!NOTE]  
>  啟用 SQLCMD 模式就會關閉 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢編輯器中的 IntelliSense 和 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 偵錯工具。  
  
 查詢編輯器中的 SQLCMD 指令碼可以使用所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼都使用的相同功能。 這些功能包括：  
  
-   色彩編碼  
  
-   執行指令碼  
  
-   原始程式碼控制  
  
-   剖析指令碼  
  
-   Showplan  
  
## <a name="enable-sqlcmd-scripting-in-query-editor"></a>在查詢編輯器中啟用 SQLCMD 指令碼  
 若要針對使用中 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器視窗開啟 SQLCMD 指令碼，請使用下列程序。  
  
#### <a name="to-switch-a-database-engine-query-editor-window-to-sqlcmd-mode"></a>將 Database Engine 查詢編輯器視窗切換到 SQLCMD 模式  
  
1.  在物件總管中，以滑鼠右鍵按一下伺服器，然後按一下 [新增查詢]  ，即可開啟新的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器視窗。  
  
2.  在 [查詢]  功能表上，按一下 [SQLCMD 模式]  。  
  
     查詢編輯器會在其本身的內容中執行 **sqlcmd** 陳述式。  
  
3.  在 [SQL 編輯器]  工具列的 [可用資料庫]  清單中，選取 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]。  
  
4.  在查詢編輯器視窗中鍵入下列兩項 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式及 `!!DIR` **sqlcmd** 陳述式：  
  
    ```  
    SELECT DISTINCT Type FROM Sales.SpecialOffer;  
    GO  
    !!DIR  
    GO  
    SELECT ProductCategoryID, Name FROM Production.ProductCategory;  
    GO  
    ```  
  
5.  按 F5 執行混合 [!INCLUDE[tsql](../../includes/tsql-md.md)] 與 MS-DOS 陳述式的整個區段。  
  
     請注意第 1 個和第 3 個陳述式產生的兩個 SQL 結果窗格。  
  
6.  在 [結果]  窗格中，按一下 [訊息]  索引標籤來查看這三個陳述式產生的訊息：  
  
    -   (6 個資料列受影響)  
  
    -   \<The directory information>  
  
    -   (4 個資料列受影響)  
  
> [!IMPORTANT]  
>  從命令列執行時， **sqlcmd** 公用程式允許與作業系統進行完整互動。 當您在 [SQLCMD 模式]**** 中使用 [查詢編輯器] 時，您必須非常小心，不要執行互動式陳述式。 [查詢編輯器] 無法回應作業系統提示。  
  
 如需有關如何執行 SQLCMD 的詳細資訊，請參閱 [sqlcmd 工用程式](../../tools/sqlcmd-utility.md)，或進入 SQLCMD 教學課程。  
  
## <a name="enable-sqlcmd-scripting-by-default"></a>依預設，會啟用 SQLCMD 指令碼  
 若要依預設開啟 SQLCMD 指令碼，請在 [工具]**** 功能表中選取 [選項]****，展開 [執行查詢]**** 和 **SQL Server**，按一下 [一般]**** 頁面，再核取 [預設會以 SQLCMD 模式開啟新查詢]**** 方塊。  
  
## <a name="writing-and-editing-sqlcmd-scripts"></a>撰寫和編輯 SQLCMD 指令碼  
 在啟用指令碼模式之後，您便可以撰寫 SQLCMD 命令和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 適用的規則如下：  
  
-   SQLCMD 命令必須是行中的第一個陳述式。  
  
-   每行只能有一個 SQLCMD 命令。  
  
-   SQLCMD 命令前面可以有註解或空格。  
  
-   不會執行註解字元內的 SQLCMD 命令。  
  
-   單行註解字元是兩個連字號 (`--)` ，必須在行首。  
  
-   作業系統命令的前面必須有兩個驚歎號 (`!!`)。 兩個驚歎號的命令會使在驚歎號後面的陳述式利用 `cmd.exe` 命令處理器來執行。 `!!` 之後的文字會當做參數傳給 `cmd.exe`，因此，最後執行的命令列是： `"%SystemRoot%\system32\cmd.exe /c <text after !!>"`。  
  
-   為了清楚區分 SQLCMD 命令和 [!INCLUDE[tsql](../../includes/tsql-md.md)]，所有 SQLCMD 命令的前面都必須加上冒號 (`:`)。  
  
-   使用 `GO` 命令時不需要前置詞或在其之前加上 `!!:`  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器支援環境變數和定義成 SQLCMD 指令碼一部分的變數，但不支援內建的 SQLCMD 或 **osql** 變數。 由 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 所處理的 SQLCMD 對變數而言，是區分大小寫的。 例如，PRINT '$(COMPUTERNAME)' 會產生正確的結果，但是 PRINT '$(ComputerName)' 會傳回錯誤。  
  
> [!CAUTION]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]SqlClient 以便在正規和 SQLCMD 模式中執行。 從命令列執行時，SQLCMD 會使用 OLE DB 提供者。 由於可能套用不同的預設選項，因此，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] SQLCMD 模式中，以及在 SQLCMD 公用程式中執行相同的查詢時，可能會出現不同的行為。  
  
## <a name="supported-sqlcmd-syntax"></a>支援的 SQLCMD 語法  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器支援下列 SQLCMD 指令碼關鍵字：  
  
 `[!!:]GO[count]`  
  
 `!! <command>`  
  
 `:exit(statement)`  
  
 `:Quit`  
  
 `:r <filename>`  
  
 `:setvar <var> <value>`  
  
 `:connect server[\instance] [-l login_timeout] [-U user [-P password]]`  
  
 `:on error [ignore|exit]`  
  
 `:error <filename>|stderr|stdout`  
  
 `:out <filename>|stderr|stdout`  
  
> [!NOTE]  
>  對於 `:error` 和 `:out`而言， `stderr` 和 `stdout` 都會將輸出傳到訊息索引標籤。  
  
 查詢編輯器不支援上面所未列出的 SQLCMD 命令。 當執行包含不支援的 SQLCMD 關鍵字之腳本時，查詢編輯器會 \<ignored command*> 針對每個不支援的關鍵字，將「忽略命令 *」訊息傳送至目的地。 指令碼將順利執行，但會忽略不支援的命令。  
  
> [!CAUTION]  
>  由於您不是從命令列啟動 SQLCMD，因此，當執行查詢編輯器的 SQLCMD 模式時，會有若干限制。 您不能傳入變數之類的命令列參數，且因為查詢編輯器沒有回應作業系統提示的能力，您必須小心避免執行互動式的陳述式。  
  
## <a name="color-coding-in-sqlcmd-scripts"></a>SQLCMD 指令碼中的色彩編碼  
 在啟用 SQLCMD 指令碼之後，指令碼會有色彩編碼。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 關鍵字的色彩編碼維持不變。 SQLCMD 命令會呈現陰影效果的背景。  
  
## <a name="example"></a>範例  
 下列範例使用 **sqlcmd** 陳述式建立名為 testoutput.txt 的輸出檔、執行兩個 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 陳述式，以及一個作業系統命令 (列印目前的目錄)。 產生的檔案包含 `DIR` 陳述式的訊息輸出，且後面會有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的結果輸出。  
  
```  
:out C:\testoutput.txt  
SELECT @@VERSION As 'Server Version'  
!!DIR  
!!:GO  
SELECT @@SERVERNAME AS 'Server Name'  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)  
  
  
