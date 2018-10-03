---
title: 資料來源範例 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 69cc3a0d32c12c71b3909bda23dea93417475f2a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847626"
---
# <a name="data-source-example"></a>資料來源範例
在執行 Microsoft® Windows NT® Server/Windows 2000 Server、 Microsoft Windows NT 工作站/Windows 2000 Professional 或 Microsoft Windows® 95/98，機器資料的電腦上來源資訊會儲存在登錄中。 根據哪一個登錄金鑰的資訊會儲存在中，資料來源就所謂*使用者資料來源*或是*系統資料來源*。 使用者資料來源會儲存在 HKEY_CURRENT_USER 機碼之下，而且僅適用於目前的使用者。 系統資料來源會儲存在 HKEY_LOCAL_MACHINE 機碼之下，而且可由一部電腦上的多個使用者。 它們也可以使用全系統服務，然後取得資料來源的存取權，即使沒有任何使用者登入電腦。 如需有關使用者和系統資料來源的詳細資訊，請參閱 < [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md)。  
  
 假設使用者具有三個使用者資料來源： 人員和清查，使用 Oracle DBMS;和薪資、 使用 Microsoft SQL Server DBMS。 資料來源的登錄值可能是：  
  
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
