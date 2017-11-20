---
title: "資料來源範例 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], examples
ms.assetid: cbf15f32-0550-4c74-8088-8f7ac3855469
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 85eae404d4fa0ab739c699c8f120c76122c8ba67
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="data-source-example"></a>資料來源範例
在執行 Microsoft® Windows NT® Server/Windows 2000 Server、 Microsoft Windows NT 工作站/Windows 2000 Professional 或 Microsoft Windows® 95/98，機器資料來源資訊會儲存在登錄中。 根據哪些登錄金鑰資訊會儲存在下，資料來源稱為*使用者資料來源*或*系統資料來源*。 使用者資料來源會儲存在 HKEY_CURRENT_USER 機碼下，而且僅適用於目前的使用者。 系統資料來源會儲存在 HKEY_LOCAL_MACHINE 機碼下，而且可由多個使用者在一部電腦上。 它們也可以使用全系統服務，然後取得資料來源的存取，即使沒有任何使用者登入電腦。 如需有關使用者和系統資料來源的詳細資訊，請參閱[SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md)。  
  
 假設使用者具有三個使用者資料來源： 人員和清查，請使用 Oracle DBMS;並使用 Microsoft SQL Server DBMS 的薪資。 資料來源的登錄值可能是：  
  
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
  
 它可能是薪資資料來源的登錄值：  
  
```  
HKEY_CURRENT_USER  
     SOFTWARE  
          ODBC  
               Odbc.ini  
                    Payroll  
                         Driver : REG_SZ : C:\WINDOWS\SYSTEM\Sqlsrvr.dll  
                         Description : REG_SZ : Payroll database  
                         Server : REG_SZ : PYRLL1  
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```

