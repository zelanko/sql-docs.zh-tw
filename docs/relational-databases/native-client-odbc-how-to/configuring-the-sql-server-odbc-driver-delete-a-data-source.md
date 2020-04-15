---
title: 刪除資料來源 (ODBC) |微軟文件
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 93ea12968c92f7849876d29d31207b8028714482
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294502"
---
# <a name="configuring-the-sql-server-odbc-driver---delete-a-data-source"></a>設定 SQL Server ODBC 驅動程式 - 刪除資料來源
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在搭配 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本使用 ODBC 應用程式以前，您必須知道如何在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上升級目錄預存程序的版本，以及加入、刪除和測試資料來源。  
  
  您可以透過使用 ODBC 管理員以程式設計方式(透過[使用 SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md))或刪除檔案(如果檔案資料來源名稱)來刪除資料來源。  
  
### <a name="to-delete-a-data-source-by-using-odbc-administrator"></a>使用 ODBC 管理員刪除資料來源  
  
1.  在**控制面板**中,打開**管理工具**,然後按**兩下 ODBC 資料來源(64 位元)** 或**ODBC 資料來源 (32 位)。** 或者，您也可以從命令提示字元執行 odbcad32.exe。  
  
2.  單擊**使用者 DSN、****系統 DSN**或**檔 DSN**選項卡。  
  
3.  選擇要刪除的資料來源。  
  
4.  按下 **「刪除**」,然後確認刪除。  

## <a name="example"></a>範例  
 要以程式設計方式刪除資料來源,請使用ODBC_REMOVE_DSN或ODBC_REMOVE_SYS_DSN作為第二個參數呼叫[SQLConfigDataSource。](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)  
  
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
 [新增資料來源&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-add-a-data-source.md)  
  
  
