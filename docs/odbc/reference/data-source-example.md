---
title: 資料來源範例 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], examples
ms.assetid: cbf15f32-0550-4c74-8088-8f7ac3855469
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 48c87f0d9f0a48b7d216151178c15bb019c0cbaa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306519"
---
# <a name="data-source-example"></a>資料來源範例
在運行 Microsoft ® Windows NT® 伺服器/Windows 2000 伺服器、微軟 Windows NT 工作站/Windows 2000 專業版或 Microsoft Windows ® 95/98 的電腦中,電腦數據源資訊存儲在註冊表中。 根據資訊儲存的註冊表項,資料來源為*使用者資料來源*或*系統資料來源*。 使用者數據源存儲在HKEY_CURRENT_USER鍵下,並且僅對當前使用者可用。 系統數據源存儲在HKEY_LOCAL_MACHINE鍵下,可以在一台計算機上由多個使用者使用。 它們也可以由系統範圍的服務使用,即使沒有用戶登錄到計算機,這些服務也可以訪問數據源。 有關使用者和系統資料來源的詳細資訊,請參閱[SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md)。  
  
 假設使用者有三個用戶數據源:使用 Oracle DBMS 的人員和清單;和工資單,它使用微軟 SQL Server DBMS。 資料來源的註冊表值可能是:  
  
```  
HKEY_CURRENT_USER  
SOFTWARE  
          ODBC  
               Odbc.ini  
                    ODBC Data Sources  
                    Personnel : REG_SZ : Oracle  
                    Inventory : REG_SZ : Oracle  
                    Payroll : REG_SZ : SQL Server  
```  
  
 工資單資料源的註冊表值可能是:  
  
```  
HKEY_CURRENT_USER  
     SOFTWARE  
          ODBC  
               Odbc.ini  
                    Payroll  
                         Driver : REG_SZ : C:\WINDOWS\SYSTEM\Sqlsrvr.dll  
                         Description : REG_SZ : Payroll database  
                         Server : REG_SZ : PYRLL1  
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```
