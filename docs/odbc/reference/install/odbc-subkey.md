---
title: ODBC 子鍵 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry entries for data sources [ODBC], ODBC subkey
- subkeys [ODBC], ODBC subkey
- ODBC subkey [ODBC]
ms.assetid: f9534144-8f42-4946-b0fb-638e9dcde9c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96e9a5f4c3cdac5097686528d3c089d9ec5826f7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287438"
---
# <a name="odbc-subkey"></a>ODBC 子機碼
ODBC 子鍵下的值指定 ODBC 跟蹤選項。 這些選項通過**SQLManageDataSource**顯示的 ODBC 資料來源管理員對話方塊的「跟蹤」選項卡進行設置。 ODBC 子金鑰本身是可選的。 這些值的格式如下表所示。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|追蹤|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*追蹤檔案路徑*|  
  
 這些值具有下表中描述的含義。  
  
|值|意義|  
|-----------|-------------|  
|追蹤|如果使用SQL_HANDLE_ENV選項調用**SQLAllocHandle**時追蹤值設置為 1,則為調用應用程式啟用跟蹤。<br /><br /> 如果追蹤關鍵字在應用程式使用SQL_HANDLE_ENV選項調用**SQLAllocHandle**時設置為 0,則禁用調用應用程式的跟蹤。 這是預設值。<br /><br /> 應用程式可以使用SQL_ATTR_TRACE連接屬性啟用或禁用跟蹤。 但是,這樣做不會更改此值的數據。|  
|TraceFile|如果啟用了跟蹤,驅動程式管理器將寫入跟蹤檔值指定的跟蹤檔。<br /><br /> 如果未指定追蹤檔案,驅動程式管理員將寫入當前驅動器上的 Sql.log 檔。 這是預設值。<br /><br /> 跟蹤應僅用於單個應用程式,或者每個應用程式應指定不同的跟蹤檔。 否則,兩個或多個應用程式將嘗試同時打開同一跟蹤文件,從而導致錯誤。<br /><br /> 應用程式可以使用SQL_ATTR_TRACEFILE連接屬性指定新的跟蹤檔。 但是,這樣做不會更改此值的數據。|  
  
 例如,假設已啟用跟蹤,並且跟蹤檔為 C:_Odbc.log。 ODBC 子鍵下的值如下所示:  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
