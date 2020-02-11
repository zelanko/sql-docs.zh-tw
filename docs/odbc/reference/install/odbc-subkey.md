---
title: ODBC 子機碼 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8aad5171b98c54aa0c4adbde1a5678e4fd953640
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093957"
---
# <a name="odbc-subkey"></a>ODBC 子機碼
ODBC 子機碼底下的值會指定 ODBC 追蹤選項。 這些選項是透過**SQLManageDataSources**所顯示的 [ODBC 資料來源管理員] 對話方塊的 [追蹤] 索引標籤來設定。 ODBC 子機碼本身是選擇性的。 這些值的格式如下表所示。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|Trace|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile-path*|  
  
 這些值具有下表中所述的意義。  
  
|值|意義|  
|-----------|-------------|  
|Trace|當應用程式使用 SQL_HANDLE_ENV 選項呼叫**SQLAllocHandle**時，如果追蹤值設定為1，則會針對呼叫應用程式啟用追蹤。<br /><br /> 當應用程式使用 SQL_HANDLE_ENV 選項呼叫**SQLAllocHandle**時，如果 Trace 關鍵字設為0，則會停用呼叫應用程式的追蹤。 這是預設值。<br /><br /> 應用程式可以使用 SQL_ATTR_TRACE 連接屬性來啟用或停用追蹤。 不過，這樣做並不會變更此值的資料。|  
|TraceFile|如果已啟用追蹤，驅動程式管理員會寫入 TraceFile 值所指定的追蹤檔案。<br /><br /> 如果未指定任何追蹤檔，驅動程式管理員會寫入目前磁片磁碟機上的 Sql .log 檔案。 這是預設值。<br /><br /> 追蹤應該僅用於單一應用程式，或每個應用程式都應該指定不同的追蹤檔案。 否則，兩個或多個應用程式會嘗試同時開啟相同的追蹤檔案，而造成錯誤。<br /><br /> 應用程式可以使用 SQL_ATTR_TRACEFILE 連接屬性來指定新的追蹤檔。 不過，這樣做並不會變更此值的資料。|  
  
 例如，假設追蹤已啟用，且追蹤檔案為 C:\Odbc.log。 ODBC 子機碼底下的值如下所示：  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
