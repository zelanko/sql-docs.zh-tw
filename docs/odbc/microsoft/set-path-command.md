---
title: SET 路徑命令 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 058f9f36aa3e762b27e2548fb1a1ddd4767399e8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="set-path-command"></a>SET 路徑命令
指定的路徑來搜尋檔案。 驅動程式特定資訊，請參閱 < 備註 >。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>引數  
 若要 [*路徑*]  
 指定您想要搜尋 Visual FoxPro 的目錄。 使用逗號或分號分隔的目錄。  
  
## <a name="remarks"></a>備註  
 設定路徑，可讓您指定其他 Visual FoxPro 程式可以呼叫預存程序內的搜尋路徑。 設定路徑不會變更您所指定的連接資料來源的路徑。  
  
 設定路徑以而不發出*路徑*還原到預設目錄或資料夾的路徑。  
  
## <a name="driver-remarks"></a>驅動程式註解  
 如果您在預存程序中發出設定路徑，它會略過下列函式與命令：  
  
-   例如，目錄函數[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)和[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)會忽略新路徑，並繼續進行至參考資料來源中所指定的路徑[SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)或[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)。  
  
-   例如選取、 INSERT、 UPDATE、 DELETE 和 CREATE TABLE 命令將會忽略新路徑並仍可繼續參考中的資料來源所指定的路徑**SQLPrepare**或**SQLExecDirect**。  
  
 如果您在預存程序中的問題設定路徑，並不後續設定回其原始狀態的路徑，其他資料庫的連接將使用新路徑，（因為設定路徑範圍不是資料的工作階段）。  
  
 如果您想要建立、 選取或更新資料表以外的資料來源所指定的目錄中，指定檔案的完整路徑，與您的命令。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 安裝程式 對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns （Visual FoxPro ODBC 驅動程式）](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect （Visual FoxPro ODBC 驅動程式）](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (Visual FoxPro ODBC Driver)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
