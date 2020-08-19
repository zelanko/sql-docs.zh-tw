---
description: SET PATH 命令
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36131e53d1a10d8af3e7ca226768a9c08a14ba77
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421832"
---
# <a name="set-path-command"></a>SET PATH 命令
指定檔案搜尋的路徑。 如需驅動程式特定的資訊，請參閱備註。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>引數  
 TO [ *Path*]  
 指定您想要 Visual FoxPro 搜尋的目錄。 使用逗號或分號來分隔目錄。  
  
## <a name="remarks"></a>備註  
 設定路徑可讓您指定可在預存程式中呼叫的其他 Visual FoxPro 程式搜尋路徑。 設定路徑不會變更您為連接所指定的資料來源路徑。  
  
 將路徑設定為沒有 *路徑* ，以還原預設目錄或資料夾的路徑。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 如果您在預存程式中發出 SET PATH，下列函數和命令將會忽略它：  
  
-   [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)和[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)等目錄函數將會忽略新的路徑，並繼續參考[SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)或[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)中的資料來源所指定的路徑。  
  
-   SELECT、INSERT、UPDATE、DELETE 和 CREATE TABLE 等命令會忽略新的路徑，並繼續參考 **SQLPrepare** 或 **SQLExecDirect**中的資料來源所指定的路徑。  
  
 如果您在預存程式中發出 SET 路徑，而且之後不將路徑設回其原始狀態，則資料庫的其他連接將會使用新路徑 (，因為設定路徑的範圍不限於資料會話) 。  
  
 如果您想要建立、選取或更新非資料來源所指定之目錄中的資料表，請使用您的命令來指定檔案的完整路徑。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Visual FoxPro 安裝程式對話方塊](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns (Visual FoxPro ODBC Driver) ](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect (Visual FoxPro ODBC Driver) ](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables (Visual FoxPro ODBC Driver)](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
