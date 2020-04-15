---
title: ODBC 可視化狐狸專業設置對話方塊 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298078"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>ODBC Visual FoxPro 設定對話方塊
**ODBC 視覺化 FoxPro 安裝程式**對話框使您能夠添加或更改 Visual FoxPro 資料來源。  
  
 要下載驅動程式,請參閱[可視化福斯Pro ODBC驅動程式下載網站](https://go.microsoft.com/fwlink/?LinkId=121318)。  
  
## <a name="dialog-box-options"></a>對話方塊選項  
 **資料來源名稱**  
 鍵入要用於數據源的名稱。  
  
 **說明**  
 鍵入數據源的說明。  
  
 **資料庫類型**  
 允許您選擇要連接到資料來源的資料庫類型。  
  
 **視覺化 FoxPro 資料庫 (.DBC)**  
 指定資料來源連接到 Visual FoxPro[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)(.dbc 檔案) 以及資料庫中的所有表和本地檢視。  
  
 **可用表表單**  
 指定資料來源連接到[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目錄。 同一目錄中的任何[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)表都將被 ODBC 目錄函數(如[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)或[SQLTables)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)忽略。 可以使用透過 SQLExecute 和[SQLExecDirect](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)發送[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)的 SQL SELECT 語句存取資料庫表。  
  
 **路徑**  
 顯示資料庫的路徑和名稱或數據源連接到的可用表的目錄。  
  
 **瀏覽**  
 使您能夠在系統和網路上搜索要連接到資料源的資料庫或目錄。  
  
 **選項**  
 展開對話框,以便可以設置 Visual FoxPro ODBC 驅動程式選項。  
  
## <a name="driver"></a>驅動程式  
 **整理序列**  
 欄位排序的順序。 預設序列反映作業系統的語言版本支援的順序。 有關支援的整理序列的清單,請參閱[SET COLLATE](../../odbc/microsoft/set-collate-command.md)。  
  
 **排除**  
 勾選此選項後,當您使用資料來源存取資料時,驅動程式將專門打開 Visual FoxPro 資料庫。 在獨佔打開資料庫時,其他用戶無法訪問資料庫或資料庫中的表。 獨佔打開的資料庫中的表將作為 SHARED 打開。 要獨佔打開表,請使用[SET 獨佔](../../odbc/microsoft/set-exclusive-command.md)命令。 當**資料庫類型**設置為**自由表目錄**時,將禁用此複選框。  
  
 **空**  
 確定使用 ALTER TABLE 和 CREATE TABLE 建立的列是否允許空值。 如果設定「空開啟」,則「插入 」 -SQL 將空值插入到插入 - SQL...VALUE 條款。 如果 Null 為 OFF,則插入空白。 還可以透過傳遞的連接字串控制此選項,如以下代碼中:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **刪除**  
 確定是否返回標記為已刪除的行。 還可以透過傳遞的連接字串控制此選項,如以下代碼中:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **在後臺提取資料**  
 確定是在後台提取記錄(逐行提取),還是應用程式將等待結果集中的所有記錄被提取。
