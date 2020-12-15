---
title: " (ODBC) 加入資料來源 |Microsoft Docs"
description: 瞭解 SQL Server ODBC 驅動程式如何使用遠端預存程序呼叫機制，以 SQL Server 中的遠端預存程式來呼叫預存程式。
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: da691dab0513ccd472459e2ad6ecaa4c446b9828
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467769"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>設定 SQL Server ODBC 驅動程式 - 新增資料來源
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  在搭配 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本使用 ODBC 應用程式以前，您必須知道如何在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上升級目錄預存程序的版本，以及加入、刪除和測試資料來源。  
  
  您可以使用 ODBC 管理員，以程式設計方式 (使用 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)) 或建立檔案，以加入資料來源。  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>使用 ODBC 管理員加入資料來源  
  
1.  從 **主控台** 中，存取系統 **管理工具** ，然後將 **odbc 資料來源 (64 位)** 或 **odbc 資料來源 (32 位)**。 或者，您可以叫用 odbcad32.exe。  
  
2.  按一下 [ **使用者 dsn**]、[ **系統 dsn**] 或 [檔案 **DSN** ] 索引標籤，然後按一下 [ **新增**]。  
  
3.  按一下 [ **SQL Server**]，然後按一下 **[完成]**。  
  
4.  完成 [ **建立新的資料來源** ] 中的步驟，以 SQL Server Wizard。  
  
### <a name="to-add-a-data-source-programmatically"></a>以程式設計方式加入資料來源  
  
1.  使用第二個參數設定為 ODBC_ADD_DSN 或 ODBC_ADD_SYS_DSN 來呼叫 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) 。  
  
### <a name="to-add-a-file-data-source"></a>加入檔案資料來源  
  
1.  在連接字串中使用 SAVEFILE = file_name 參數來呼叫 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 。 如果連接成功，ODBC 驅動程式會利用 SAVEFILE 參數所指向位置中的連接參數建立檔案資料來源。  
  
## <a name="see-also"></a>另請參閱  
[&#40;ODBC&#41;刪除資料來源 ](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
