---
title: 設定 PATH 指令 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e44093c3ea18bc995264a8974726f5af0abe3b3a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300818"
---
# <a name="set-path-command"></a>SET PATH 命令
指定檔搜索的路徑。 有關特定於驅動程序的資訊,請參閱備註。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>引數  
 到 %*11 的路徑*  
 指定您希望 Visual FoxPro 搜尋的目錄。 使用逗號或分號分隔目錄。  
  
## <a name="remarks"></a>備註  
 SET PATH 允許您為可在儲存過程中調用的其他 Visual FoxPro 程式指定搜索路徑。 SET PATH 不會更改您為連接指定的數據源的路徑。  
  
 發出「設定路徑到無*路徑*」以還原預設目錄或資料夾的路徑。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 如果在儲存過程中發出 SET PATH,則以下函數和指令將忽略它:  
  
-   目錄函數(如[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)和[SQLColumns)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)將忽略新路徑,並繼續參考[SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)或[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)中資料來源指定的路徑。  
  
-   選擇、插入、更新、刪除和創建表等命令將忽略新路徑,並繼續引用**SQLPrepare**或**SQLExecDirect**中資料來源指定的路徑。  
  
 如果在儲存過程中發出 SET PATH,並且隨後未將路徑設置為其原始狀態,則到資料庫的其他連接將使用新路徑(因為 SET PATH 未限定為數據會話)。  
  
 如果要在目錄中創建、選擇或更新資料來源指定的表以外的表,請使用命令指定檔的完整路徑。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 視覺化狐狸專業設定對話框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQL柱 (視覺化福斯 Pro ODBC 驅動程式)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriver 連線(視覺化福斯Pro ODBC驅動程式)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (Visual FoxPro ODBC Driver)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
