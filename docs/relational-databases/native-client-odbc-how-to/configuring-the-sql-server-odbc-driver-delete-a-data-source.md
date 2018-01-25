---
title: "刪除資料來源 (ODBC) |Microsoft 文件"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: data sources [ODBC]
ms.assetid: 910e3e16-7b91-49d8-80bb-b4243926afaa
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a86c74ec8ebaec54801b045202469a217a4c4bf7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="configuring-the-sql-server-odbc-driver---delete-a-data-source"></a>設定 SQL Server ODBC 驅動程式-刪除資料來源
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在搭配 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本使用 ODBC 應用程式以前，您必須知道如何在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上升級目錄預存程序的版本，以及加入、刪除和測試資料來源。  
  
  您可以刪除資料來源使用 ODBC 管理員，以程式設計方式 (使用[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md))，或刪除檔案 （如果是檔案資料來源名稱）。  
  
### <a name="to-delete-a-data-source-by-using-odbc-administrator"></a>使用 ODBC 管理員刪除資料來源  
  
1.  在**控制台**，開啟**系統管理工具**，然後按兩下  **ODBC 資料來源 （64 位元）**或**ODBC 資料來源 （32 位元）**. 或者，您也可以從命令提示字元執行 odbcad32.exe。  
  
2.  按一下**使用者 DSN**，**系統 DSN**，或**檔案 DSN**  索引標籤。  
  
3.  選取要刪除的資料來源。  
  
4.  按一下**移除**，然後確認刪除。  
  
## <a name="example"></a>範例  
 若要以程式設計方式刪除資料來源，請呼叫[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)使用 ODBC_REMOVE_DSN 或 ODBC_REMOVE_SYS_DSN 做為第二個參數。  
  
 下列範例會示範如何以程式設計的方式刪除資料來源。  
  
```  
// remove_odbc_data_source.cpp  
// compile with: ODBCCP32.lib user32.lib  
#include <iostream>  
#include \<windows.h>  
#include \<odbcinst.h>  
  
int main() {   
   LPCSTR provider = "SQL Server";   // Windows SQL Server Driver  
   LPCSTR provider = "SQL Server";   // Windows SQL Server driver  
   LPCSTR provider2 = "SQL Server Native Client 11.0";   // SQL Server 2012 Native Client driver  
   LPCSTR dsnname = "DSN=data2";  
   BOOL retval = SQLConfigDataSource(NULL, ODBC_REMOVE_DSN, provider, dsnname);  
   std::cout << retval;   // 1 if successful  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [新增資料來源 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-add-a-data-source.md)  
  
  
