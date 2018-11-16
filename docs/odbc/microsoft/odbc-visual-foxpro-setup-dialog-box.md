---
title: ODBC Visual FoxPro 設定對話方塊 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e2d83f77f8bb9227daab996e425d1880d1bfabd
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51674410"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro 設定對話方塊
**ODBC Visual FoxPro 設定**對話方塊可讓您新增或變更 Visual FoxPro 資料來源。  
  
 若要下載此驅動程式，請參閱[Visual FoxPro ODBC Driver 下載網站](https://go.microsoft.com/fwlink/?LinkId=121318)。  
  
## <a name="dialog-box-options"></a>對話方塊選項  
 **資料來源名稱**  
 輸入您想要使用資料來源的名稱。  
  
 **說明**  
 輸入資料來源的描述。  
  
 **資料庫類型**  
 可讓您選擇您想要連接到資料來源之資料庫類型。  
  
 **Visual FoxPro 資料庫 (。雙位元組字元）**  
 指定的資料來源連接至 Visual FoxPro[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)（.dbc 檔案） 和所有的資料表和資料庫中的本機檢視。  
  
 **可用的資料表目錄**  
 指定的資料來源連接至的目錄[免費資料表](../../odbc/microsoft/visual-foxpro-terminology.md)。 任何[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)相同的目錄中的資料表會如 ODBC 目錄函數忽略[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)或是[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)。 使用透過傳送的 SQL SELECT 陳述式也可以存取資料庫資料表[SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)並[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)。  
  
 **路徑**  
 顯示的路徑和名稱的資料庫或資料來源連接的可用資料表的目錄。  
  
 **瀏覽**  
 可讓您搜尋您的系統和網路，以您要連接到資料來源目錄的資料庫。  
  
 **選項。**  
 因此，您可以設定 Visual FoxPro ODBC Driver 選項，請展開對話方塊。  
  
## <a name="driver"></a>驅動程式  
 **定序順序**  
 欄位的排序順序。 預設順序會反映您的作業系統語言版本所支援的序列。 如需支援的定序順序的清單，請參閱 <<c0> [ 設定定序](../../odbc/microsoft/set-collate-command.md)。  
  
 **排除**  
 選取此核取方塊時，驅動程式會以獨佔方式存取使用的資料來源的資料時，才開啟 Visual FoxPro 資料庫。 資料庫以獨佔方式開啟時，其他使用者無法存取資料庫或資料庫中的資料表。 以獨佔方式開啟的資料庫中的資料表會開啟為 SHARED。 若要以獨佔方式開啟資料表，請使用[獨佔設定](../../odbc/microsoft/set-exclusive-command.md)命令。 此核取方塊已停用時**資料庫類型**設為**免費資料表目錄**。  
  
 **Null**  
 決定是否使用 ALTER TABLE 和 CREATE TABLE 所建立的資料行允許 null 值。 如果您設為 Null 的 ON，INSERT-SQL 會將 null 值插入 INSERT-SQL 中不包含任何資料行...VALUE 子句。 如果 Null 是 OFF，則會插入空白。 您也可以控制這個選項，透過傳遞的連接字串，如下列程式碼所示：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **刪除**  
 決定是否要傳回標示為已刪除的資料列。 您也可以控制這個選項，透過傳遞的連接字串，如下列程式碼所示：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **在背景中擷取資料**  
 決定是否將在背景 （漸進式擷取） 中擷取記錄，或您的應用程式會等候，直到擷取結果集中的所有記錄。
