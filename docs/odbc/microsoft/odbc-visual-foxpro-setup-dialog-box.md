---
title: ODBC Visual FoxPro 安裝程式對話方塊 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef7ac702a69342833c6dfffa0ffc9cdd0ac2857e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298078"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro 設定對話方塊
[ **ODBC Visual FoxPro 安裝程式**] 對話方塊可讓您加入或變更 Visual foxpro 資料來源。  
  
 若要下載驅動程式，請參閱[Visual FOXPRO ODBC driver 下載網站](https://go.microsoft.com/fwlink/?LinkId=121318)。  
  
## <a name="dialog-box-options"></a>對話方塊選項  
 **資料來源名稱**  
 輸入您想要用於資料來源的名稱。  
  
 **說明**  
 輸入資料來源的描述。  
  
 **資料庫類型**  
 讓您選擇要讓資料來源連接的資料庫類型。  
  
 **Visual FoxPro 資料庫（。DBC**  
 指定資料來源連接到 Visual FoxPro[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)（dbc 檔案）以及資料庫中的所有資料表和本機視圖。  
  
 **免費資料表目錄**  
 指定資料來源連接到[可用資料表](../../odbc/microsoft/visual-foxpro-terminology.md)的目錄。 ODBC 目錄函數（例如[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)或[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)）會忽略相同目錄中的任何[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)資料表。 您可以使用透過[SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)和[SQLEXECDIRECT](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)傳送的 SQL SELECT 語句來存取資料庫資料表。  
  
 **路徑**  
 顯示資料庫的路徑和名稱，或資料來源連接的可用資料表目錄。  
  
 **瀏覽**  
 可讓您針對要連接資料來源的資料庫或目錄，搜尋您的系統和網路。  
  
 **選項**  
 展開對話方塊，讓您可以設定 Visual FoxPro ODBC 驅動程式選項。  
  
## <a name="driver"></a>驅動程式  
 **排序次序**  
 排序欄位的順序。 預設順序會反映您的作業系統語言版本所支援的序列。 如需支援的定序序列清單，請參閱[SET COLLATE](../../odbc/microsoft/set-collate-command.md)。  
  
 **排除**  
 如果選取此核取方塊，當您使用資料來源存取資料時，驅動程式會以獨佔方式開啟 Visual FoxPro 資料庫。 當資料庫以獨佔方式開啟時，其他使用者就無法存取資料庫或資料庫中的資料表。 以共用方式開啟獨佔開啟資料庫中的資料表。 若要以獨佔方式開啟資料表，請使用[SET EXCLUSIVE](../../odbc/microsoft/set-exclusive-command.md)命令。 當**資料庫類型**設定為 [**免費資料表目錄**] 時，就會停用此核取方塊。  
  
 **Null**  
 判斷使用 ALTER TABLE 和 CREATE TABLE 建立的資料行是否允許 null 值。 如果您將 Null 設為 ON，則 INSERT-SQL 會將 null 值插入至不包含在 INSERT-SQL 中的任何資料行 .。。VALUE 子句。 如果 Null 已關閉，則會插入空白。 您也可以透過傳遞的連接字串來控制此選項，如下列程式碼所示：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **刪除**  
 判斷是否傳回標示為已刪除的資料列。 您也可以透過傳遞的連接字串來控制此選項，如下列程式碼所示：  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **在背景中提取資料**  
 判斷記錄是否會在背景中提取（漸進式提取），或您的應用程式將會等候，直到提取結果集中的所有記錄為止。
