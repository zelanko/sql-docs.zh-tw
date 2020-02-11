---
title: 設定路徑命令 |Microsoft Docs
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
ms.openlocfilehash: 57685731bc5eb86381816d0cbb91a4942b5bfeff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063643"
---
# <a name="set-path-command"></a>SET PATH 命令
指定檔案搜尋的路徑。 如需驅動程式特定的資訊，請參閱備註。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>引數  
 至 [*路徑*]  
 指定您想要 Visual FoxPro 搜尋的目錄。 請使用逗號或分號來分隔目錄。  
  
## <a name="remarks"></a>備註  
 [設定路徑] 可讓您指定可在預存程式內呼叫之其他 Visual FoxPro 程式的搜尋路徑。 [設定路徑] 不會變更您為連接所指定的資料來源路徑。  
  
 問題：將路徑設定為不含*路徑*，以還原預設目錄或資料夾的路徑。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 如果您在預存程式中發出 SET PATH，則下列函式和命令會忽略它：  
  
-   目錄函式（例如[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)和[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) ）將會忽略新的路徑，並繼續參考[SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)或[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)中的資料來源所指定的路徑。  
  
-   [選取]、[插入]、[更新]、[刪除] 和 [CREATE TABLE] 等命令會忽略新的路徑，並繼續參考**SQLPrepare**或**SQLExecDirect**中的資料來源所指定的路徑。  
  
 如果您在預存程式中發出 SET PATH，而之後又不將路徑設回其原始狀態，則其他資料庫連接將會使用新的路徑（因為 SET PATH 的範圍不是資料會話）。  
  
 如果您想要建立、選取或更新目錄中的資料表，而非由資料來源所指定，請使用您的命令指定該檔案的完整路徑。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 安裝程式對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns （Visual FoxPro ODBC Driver）](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect （Visual FoxPro ODBC Driver）](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (Visual FoxPro ODBC Driver)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
