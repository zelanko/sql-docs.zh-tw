---
title: "ODBC Visual FoxPro 安裝程式對話方塊 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 22208bd706e7b8966f54a501e9580b35d99a0555
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro 安裝程式 對話方塊
**ODBC Visual FoxPro 安裝**對話方塊可讓您新增或變更 Visual FoxPro 資料來源。  
  
 若要下載此驅動程式，請參閱[Visual FoxPro ODBC 驅動程式下載網站](http://go.microsoft.com/fwlink/?LinkId=121318)。  
  
## <a name="dialog-box-options"></a>對話方塊選項  
 **資料來源名稱**  
 輸入您想要使用資料來源的名稱。  
  
 **說明**  
 輸入資料來源的描述。  
  
 **資料庫類型**  
 可讓您選擇您想要連接到您資料來源之資料庫類型。  
  
 **Visual FoxPro 資料庫 (。雙位元組字元）**  
 指定資料來源連接至 Visual FoxPro[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)（.dbc 檔案） 以及所有資料表和本機資料庫中的檢視。  
  
 **可用的資料表目錄**  
 指定資料來源連接的目錄[釋放資料表](../../odbc/microsoft/visual-foxpro-terminology.md)。 任何[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)資料表相同的目錄中會如 ODBC 目錄函數忽略[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)或[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)。 使用透過傳送的 SQL SELECT 陳述式也可以存取資料庫資料表[SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)和[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)。  
  
 **路徑**  
 顯示的路徑和名稱的資料庫或資料來源連接的可用資料表的目錄。  
  
 **瀏覽**  
 可讓您搜尋您的系統和網路，以您要連接到資料來源目錄的資料庫。  
  
 **選項。**  
 展開對話方塊中，使您可以設定 Visual FoxPro ODBC 驅動程式選項。  
  
## <a name="driver"></a>驅動程式  
 **定序順序**  
 欄位的排序順序。 預設順序會反映您的作業系統語言版本所支援的序列。 如需支援的定序順序的清單，請參閱[設定 COLLATE](../../odbc/microsoft/set-collate-command.md)。  
  
 **排除**  
 選取此核取方塊時，驅動程式會以獨佔方式存取使用的資料來源的資料時，才開啟 Visual FoxPro 資料庫。 其他使用者無法存取資料庫或資料庫中的資料表時資料庫以獨佔方式開啟。 以獨佔方式開啟的資料庫中的資料表開啟為 SHARED。 若要以獨佔方式開啟資料表，使用[設定獨佔](../../odbc/microsoft/set-exclusive-command.md)命令。 已停用此核取方塊時**資料庫類型**設**可用資料表目錄**。  
  
 **Null**  
 決定是否使用 ALTER TABLE 和 CREATE TABLE 所建立的資料行允許 null 值。 如果您設為 Null 的 ON，INSERT – SQL 會將 null 值插入 INSERT – SQL 中不包含任何資料行...VALUE 子句。 如果 Null 是 OFF，則會插入空白。 您也可以控制這個選項，透過傳遞的連接字串，如下列程式碼所示：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **刪除**  
 決定是否要傳回資料列標示為已刪除。 您也可以控制這個選項，透過傳遞的連接字串，如下列程式碼所示：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **在背景中擷取資料**  
 判斷記錄將會提取在背景 （漸進式擷取） 或您的應用程式會等候，直到提取結果集內的所有記錄。
