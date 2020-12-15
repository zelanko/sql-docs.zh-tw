---
title: " (ODBC) 刪除資料來源 |Microsoft Docs"
description: 瞭解如何在使用 ODBC 應用程式搭配 SQL Server 2005 或更新版本之前，以程式設計方式使用 ODBC 管理員或使用檔案來刪除資料來源。
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: 910e3e16-7b91-49d8-80bb-b4243926afaa
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 56b013873ef8060101e28d9b2c4609fa41c0c798
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467809"
---
# <a name="configuring-the-sql-server-odbc-driver---delete-a-data-source"></a>設定 SQL Server ODBC 驅動程式 - 刪除資料來源
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  在搭配 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本使用 ODBC 應用程式以前，您必須知道如何在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上升級目錄預存程序的版本，以及加入、刪除和測試資料來源。  
  
  您可以使用 ODBC 管理員，以程式設計方式 (使用 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)) ，或藉由刪除檔案 (（如果檔案資料來源名稱) ）來刪除資料來源。  
  
### <a name="to-delete-a-data-source-by-using-odbc-administrator"></a>使用 ODBC 管理員刪除資料來源  
  
1.  在 **主控台** 中，開啟 [系統 **管理工具**]，然後按兩下 [ **odbc 資料來源] (64 位)** 或 [ **odbc 資料來源] (32 位)**。 或者，您也可以從命令提示字元執行 odbcad32.exe。  
  
2.  按一下 [ **使用者 dsn**]、[ **系統 dsn**] 或 [檔案 **DSN** ] 索引標籤。  
  
3.  選取要刪除的資料來源。  
  
4.  按一下 [ **移除**]，然後確認刪除。  

## <a name="example"></a>範例  
 若要以程式設計方式刪除資料來源，請使用 ODBC_REMOVE_DSN 或 ODBC_REMOVE_SYS_DSN 做為第二個參數來呼叫 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) 。  
  
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
 [將資料來源加入 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-add-a-data-source.md)  
  
  
