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
manager: craigg
ms.openlocfilehash: ee7cf624e7c118a5d9ef36738c810aecc4ec5684
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711536"
---
# <a name="odbc-subkey"></a>ODBC 子機碼
ODBC 子機碼底下的值會指定 ODBC 追蹤選項。 透過 [ODBC 資料來源管理員] 對話方塊，即可顯示 [追蹤] 索引標籤設定這些選項**SQLManageDataSources**。 ODBC 子機碼本身是選擇性的。 這些值的格式會是下表所示。  
  
|名稱|資料類型|data|  
|----------|---------------|----------|  
|追蹤|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile 路徑*|  
  
 的值具有下表中所述的意義。  
  
|值|意義|  
|-----------|-------------|  
|追蹤|如果追蹤值設定為 1 應用程式呼叫**SQLAllocHandle** SQL_HANDLE_ENV 選項時，呼叫應用程式啟用追蹤。<br /><br /> 當應用程式呼叫時，如果要追蹤關鍵字設定為 0 **SQLAllocHandle** SQL_HANDLE_ENV 選項時，已停用追蹤呼叫應用程式。 這是預設值。<br /><br /> 應用程式可以啟用或停用追蹤 SQL_ATTR_TRACE 連接屬性。 不過，這麼做因此不會變更此值的資料。|  
|TraceFile|如果啟用追蹤時，驅動程式管理員會寫入 TraceFile 值所指定的追蹤檔案。<br /><br /> 如果未不指定任何追蹤檔案，則驅動程式管理員寫入 Sql.log 檔案目前的磁碟機上。 這是預設值。<br /><br /> 追蹤應僅用於單一應用程式，或每個應用程式應指定不同的追蹤檔案。 否則，兩個或多個應用程式會嘗試開啟相同的追蹤檔案在此同時，導致錯誤發生。<br /><br /> 應用程式可以使用 SQL_ATTR_TRACEFILE 連接屬性指定新的追蹤檔案。 不過，這麼做因此不會變更此值的資料。|  
  
 例如，假設已啟用追蹤，並在追蹤檔案是 C:\Odbc.log。 ODBC 子機碼底下的值應如下所示：  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
