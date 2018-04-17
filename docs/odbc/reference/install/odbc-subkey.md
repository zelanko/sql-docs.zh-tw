---
title: ODBC 子機碼 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- registry entries for data sources [ODBC], ODBC subkey
- subkeys [ODBC], ODBC subkey
- ODBC subkey [ODBC]
ms.assetid: f9534144-8f42-4946-b0fb-638e9dcde9c8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a78553cbf67f4056ac50db78b0249189f2e27f26
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-subkey"></a>ODBC 子機碼
ODBC 子機碼下的值會指定 ODBC 追蹤選項。 透過 ODBC 資料來源管理員 對話方塊，即可顯示 追蹤 索引標籤設定這些選項**SQLManageDataSources**。 在 ODBC 子機碼本身是選擇性的。 這些值的格式為下表所示。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|Trace|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile 路徑*|  
  
 值的意義如下表所示。  
  
|Value|意義|  
|-----------|-------------|  
|Trace|如果追蹤值設定為 1 應用程式呼叫**SQLAllocHandle** SQL_HANDLE_ENV 選項時，呼叫應用程式啟用追蹤。<br /><br /> 當應用程式呼叫時，如果要追蹤關鍵字設定為 0 **SQLAllocHandle** SQL_HANDLE_ENV 選項時，已停用追蹤呼叫應用程式。 這是預設值。<br /><br /> 應用程式可以啟用或停用追蹤，附帶 SQL_ATTR_TRACE 連接屬性。 不過，這樣做，不會變更此值的資料。|  
|TraceFile|如果啟用追蹤時，驅動程式管理員會寫入 TraceFile 值所指定的追蹤檔案。<br /><br /> 如果未不指定任何追蹤檔案，則驅動程式管理員寫入 Sql.log 檔案目前的磁碟機上。 這是預設值。<br /><br /> 追蹤應該只能用於單一應用程式，或每個應用程式應該指定不同的追蹤檔案。 否則，兩個或多個應用程式將嘗試開啟相同的追蹤檔案在相同的時間，導致錯誤發生。<br /><br /> SQL_ATTR_TRACEFILE 連接屬性的應用程式可以指定新的追蹤檔案。 不過，這樣做，不會變更此值的資料。|  
  
 例如，假設已啟用追蹤，追蹤檔案是 C:\Odbc.log。 ODBC 子機碼下的值應如下所示：  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
