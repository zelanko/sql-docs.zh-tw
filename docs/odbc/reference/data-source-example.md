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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 48c87f0d9f0a48b7d216151178c15bb019c0cbaa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306519"
---
# <a name="data-source-example"></a>資料來源範例
在執行 Microsoft® Windows NT® Server/Windows 2000 Server、Microsoft Windows NT 工作站/Windows 2000 Professional 或 Microsoft Windows®95/98 的電腦上，電腦資料來源資訊會儲存在登錄中。 視資訊儲存所在的登錄機碼而定，資料來源稱為*使用者資料來源*或*系統資料來源*。 使用者資料來源會儲存在 HKEY_CURRENT_USER 金鑰底下，而且僅供目前使用者使用。 系統資料來源會儲存在 HKEY_LOCAL_MACHINE 的索引鍵之下，而且可以由一部電腦上的多個使用者使用。 它們也可以由全系統服務使用，如此一來，即使沒有任何使用者登入電腦，也可以取得資料來源的存取權。 如需有關使用者和系統資料來源的詳細資訊，請參閱[SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md)。  
  
 假設使用者有三個使用者資料來源：人員和清查，這會使用 Oracle DBMS;並使用 Microsoft SQL Server DBMS 的薪資。 資料來源的登錄值可能是：  
  
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
  
 而薪資資料來源的登錄值可能是：  
  
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
