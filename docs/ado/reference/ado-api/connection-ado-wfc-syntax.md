---
description: Connection (ADO - WFC 語法)
title: Connection (ADO-WFC 語法) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Connection collection [ADO], ADO/WFC syntax
ms.assetid: 8cfc35bb-91e2-47da-ad4c-982e9162cd51
author: rothja
ms.author: jroth
ms.openlocfilehash: 4a9d467a2ab9073bd287fd0cf6a3fc36c60cabda
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444520"
---
# <a name="connection-ado---wfc-syntax"></a>Connection (ADO - WFC 語法)
## <a name="package-commswfcdata"></a>封裝 .com. 資料  
  
### <a name="constructor"></a>建構函式  
  
```  
public Connection()  
public Connection(String connectionstring)  
```  
  
### <a name="methods"></a>方法  
  
```  
public int beginTrans()  
public void commitTrans()  
public void rollbackTrans()  
public void cancel()  
public void close()  
public com.ms.wfc.data.Recordset execute(String commandText)  
public com.ms.wfc.data.Recordset execute(String commandText, int options)  
public int executeUpdate(String commandText)  
public int executeUpdate(String commandText, int options)  
```  
  
 **ExecuteUpdate**方法是特殊的案例方法，會使用特定參數來呼叫基礎 ADO **execute**方法。 **ExecuteUpdate**方法不支援傳回**記錄集**物件，因此會使用**AdoEnums.ExecuteOptions**修改**execute**方法的*options*參數。 **Execute**方法完成之後，其更新的*RecordsAffected*參數會傳回給**executeUpdate**方法，最後會以**int**傳回。  
  
```  
public void open()   
public void open(String connectionString)  
public void open(String connectionString, String userID)  
public void open(String connectionString, String userID, String password)  
public void open(String connectionString, String userID, String password, int options)  
public Recordset openSchema(int schema, Object[]  
    restrictions, String schemaID)  
public Recordset openSchema(int schema)  
public Recordset openSchema(int schema, Object[] restrictions)  
```  
  
### <a name="properties"></a>屬性  
  
```  
public int getAttributes()  
public void setAttributes(int attr)  
public int getCommandTimeout()  
public void setCommandTimeout(int timeout)  
public String getConnectionString()  
public void setConnectionString(String con)  
public int getConnectionTimeout()  
public void setConnectionTimeout(int timeout)  
public int getCursorLocation()  
public void setCursorLocation(int cursorLoc)  
public String getDefaultDatabase()  
public void setDefaultDatabase(String db)  
public int getIsolationLevel()  
public void setIsolationLevel(int level)  
public int getMode()  
public void setMode(int mode)  
public String getProvider()  
public void setProvider(String provider)  
public int getState()  
public String getVersion()  
public AdoProperties getProperties()  
public com.ms.wfc.data.Errors getErrors()  
```  
  
### <a name="events"></a>事件  
 如需 ADO/WFC 事件的詳細資訊，請參閱 [Ado 事件具現化（依語言](../../../ado/guide/data/ado-event-instantiation-by-language.md)）。  
  
```  
public void addOnBeginTransComplete(ConnectionEventHandler handler)  
public void removeOnBeginTransComplete(ConnectionEventHandler handler)  
public void addOnCommitTransComplete(ConnectionEventHandler handler)  
public void removeOnCommitTransComplete(ConnectionEventHandler handler)  
public void addOnConnectComplete(ConnectionEventHandler handler)  
public void removeOnConnectComplete(ConnectionEventHandler handler)  
public void addOnDisconnect(ConnectionEventHandler handler)  
public void removeOnDisconnect(ConnectionEventHandler handler)  
public void addOnExecuteComplete(ConnectionEventHandler handler)  
public void removeOnExecuteComplete(ConnectionEventHandler handler)  
public void addOnInfoMessage(ConnectionEventHandler handler)  
public void removeOnInfoMessage(ConnectionEventHandler handler)  
public void addOnRollbackTransComplete(ConnectionEventHandler handler)  
public void removeOnRollbackTransComplete(ConnectionEventHandler handler)  
public void addOnWillConnect(ConnectionEventHandler handler)  
public void removeOnWillConnect(ConnectionEventHandler handler)  
public void addOnWillExecute(ConnectionEventHandler handler)  
public void removeOnWillExecute(ConnectionEventHandler handler)  
```  
  
## <a name="see-also"></a>另請參閱  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
