---
title: 新增資料來源 (ODBC) |微軟文件
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 55ae4f357aa850f6b3ff4ba9cca0b59a2ccbc570
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298314"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>設定 SQL Server ODBC 驅動程式 - 新增資料來源
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在搭配 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本使用 ODBC 應用程式以前，您必須知道如何在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上升級目錄預存程序的版本，以及加入、刪除和測試資料來源。  
  
  您可以透過使用 ODBC 管理員以程式設計方式(使用[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md))或建立檔案來添加資料來源。  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>使用 ODBC 管理員加入資料來源  
  
1.  從**控制面板**,存**取管理工具**,然後存取**ODBC 資料來源 (64 位元)** 或**ODBC 資料來源 (32 位)。** 或者，您可以叫用 odbcad32.exe。  
  
2.  單擊**使用者 DSN,****系統 DSN**或**檔案 DSN**選項卡,然後單擊「**添加**」 。。  
  
3.  按**下 SQL 伺服器**,然後按下 **「完成**」。  
  
4.  完成 **「向 SQL 伺服器創建新資料來源**」中的步驟。  
  
### <a name="to-add-a-data-source-programmatically"></a>以程式設計方式加入資料來源  
  
1.  使用第二個參數設置為ODBC_ADD_DSN或ODBC_ADD_SYS_DSN調用[SQLConfigDataSource。](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)  
  
### <a name="to-add-a-file-data-source"></a>加入檔案資料來源  
  
1.  使用連接字串中的 SAVEFILE_file_name 參數呼叫[SQLDriverConnect。](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 如果連接成功，ODBC 驅動程式會利用 SAVEFILE 參數所指向位置中的連接參數建立檔案資料來源。  
  
## <a name="see-also"></a>另請參閱  
[刪除資料來源&#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
