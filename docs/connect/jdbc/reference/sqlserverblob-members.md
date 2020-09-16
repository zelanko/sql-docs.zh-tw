---
description: SQLServerBlob 成員
title: SQLServerBlob 成員 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 90e48555-ea83-4a90-80a3-51bc685015ec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 223ed92379cce4baf294e7cdf6b16654aaa8fd49
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462682"
---
# <a name="sqlserverblob-members"></a>SQLServerBlob 成員
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  下表列出由 [SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md) 類別公開的成員。  
  
## <a name="constructors"></a>建構函式  
  
|名稱|描述|  
|----------|-----------------|  
|[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-constructor-sqlserverconnection-byte.md)|初始化 SQLServerBlob 類別的新執行個體。|  
  
## <a name="fields"></a>欄位  
 無。  
  
## <a name="inherited-fields"></a>繼承的欄位  
 無。  
  
## <a name="methods"></a>方法  
  
|名稱|描述|  
|----------|-----------------|  
|[free](../../../connect/jdbc/reference/free-method-sqlserverblob.md)|這個方法會釋放 BLOB 物件並且釋出它所保留的資源。|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlserverblob.md)|傳回輸入資料流，以便從 BLOB 讀取資料。|  
|[getBytes](../../../connect/jdbc/reference/getbytes-method-sqlserverblob.md)|取得 BLOB 資料來當做位元組陣列。|  
|[length](../../../connect/jdbc/reference/length-method-sqlserverblob.md) (長度)|傳回 BLOB 物件中的位元組數目。|  
|[position](../../../connect/jdbc/reference/position-method-sqlserverblob.md)|依據給定模式和開始索引，傳回指定之模式在 BLOB 中的位置。|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-method-sqlserverblob.md)|擷取可用來寫入至 BLOB 值的資料流。|  
|[setBytes](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)|從給定位置開始將給定位元組陣列寫入 BLOB，然後傳回寫入的位元組數目。|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlserverblob.md)|依給定長度截斷 BLOB。|  
  
## <a name="inherited-methods"></a>繼承的方法  
  
|類別繼承自：|方法|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerBlob 類別](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
