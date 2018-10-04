---
title: SET PATH 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3d810e66249779b2d3706e92ea39f89a0f87cff
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727546"
---
# <a name="set-path-command"></a>SET PATH 命令
指定的路徑來搜尋檔案。 驅動程式專屬資訊，請參閱 < 備註 >。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>引數  
 以 [*路徑*]  
 指定您想要搜尋的 Visual FoxPro 的目錄。 使用逗號或分號分隔的目錄。  
  
## <a name="remarks"></a>備註  
 設定路徑可讓您指定其他的 Visual FoxPro 程式可以呼叫預存程序內的搜尋路徑。 設定路徑不會變更您所指定的連接資料來源的路徑。  
  
 發給設定路徑不含*路徑*若要還原預設目錄或資料夾的路徑。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 如果您在預存程序中發出 SET PATH，它將會忽略下列函數和命令：  
  
-   目錄函式，例如[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)並[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)會忽略新的路徑，並仍可繼續參考中的資料來源所指定的路徑[SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)或[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)。  
  
-   命令，例如 SELECT、 INSERT、 UPDATE、 DELETE 與 CREATE TABLE 會忽略新的路徑，並仍可繼續參考中的資料來源所指定的路徑**SQLPrepare**或是**SQLExecDirect**。  
  
 如果您在預存程序中發出 SET PATH 並沒有後續設定回其原始狀態的路徑，其他資料庫的連接將使用新的路徑 （因為資料的工作階段不侷限 SET PATH）。  
  
 如果您想要建立、 選取，或更新以外，資料來源所指定的目錄中的資料表，請與您的命令中指定檔案的完整路徑。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 設定對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (Visual FoxPro ODBC Driver)](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (Visual FoxPro ODBC Driver)](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (Visual FoxPro ODBC Driver)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
