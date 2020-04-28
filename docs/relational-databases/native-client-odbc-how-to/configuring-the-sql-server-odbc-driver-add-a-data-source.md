---
title: 加入資料來源（ODBC） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298314"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>設定 SQL Server ODBC 驅動程式 - 新增資料來源
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在搭配 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本使用 ODBC 應用程式以前，您必須知道如何在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上升級目錄預存程序的版本，以及加入、刪除和測試資料來源。  
  
  您可以使用 ODBC 管理員，以程式設計方式（藉由使用[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)）或藉由建立檔案來加入資料來源。  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>使用 ODBC 管理員加入資料來源  
  
1.  從 [**控制台**] 中，存取 [系統**管理工具**]，然後按 [ **odbc 資料來源（64位）** ] 或 **[odbc 資料來源（32位）**]。 或者，您可以叫用 odbcad32.exe。  
  
2.  按一下 [**使用者 DSN**]、[**系統 DSN**] 或 [檔案**DSN** ] 索引標籤，然後按一下 [**新增**]。  
  
3.  按一下 [ **SQL Server**]，然後按一下 **[完成]**。  
  
4.  完成 [**建立新的資料來源以 SQL Server** Wizard] 中的步驟。  
  
### <a name="to-add-a-data-source-programmatically"></a>以程式設計方式加入資料來源  
  
1.  呼叫[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) ，並將第二個參數設定為 ODBC_ADD_DSN 或 ODBC_ADD_SYS_DSN。  
  
### <a name="to-add-a-file-data-source"></a>加入檔案資料來源  
  
1.  在連接字串中使用 SAVEFILE = file_name 參數來呼叫[SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 。 如果連接成功，ODBC 驅動程式會利用 SAVEFILE 參數所指向位置中的連接參數建立檔案資料來源。  
  
## <a name="see-also"></a>另請參閱  
[刪除 &#40;ODBC&#41;的資料來源](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
