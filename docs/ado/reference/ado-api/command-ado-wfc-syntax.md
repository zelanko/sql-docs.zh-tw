---
description: Command (ADO - WFC 語法)
title: 命令 (ADO-WFC 語法) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Command collection [ADO], ADO/WFC syntax
ms.assetid: 39d0aa06-03ac-4c9a-8400-83947756ef99
author: rothja
ms.author: jroth
ms.openlocfilehash: 09d880b305d5325120325407c5ec07e0a4e40c42
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776167"
---
# <a name="command-ado---wfc-syntax"></a>Command (ADO - WFC 語法)
## <a name="package-commswfcdata"></a>封裝 .com. 資料  
  
### <a name="constructor"></a>建構函式  
  
```  
public Command()  
public Command(String commandtext)  
```  
  
### <a name="methods"></a>方法  
  
```  
public void cancel()  
public com.ms.wfc.data.Parameter createParameter(String  
    Name, int Type, int Direction, int Size, Object Value)  
public Recordset execute()  
public Recordset execute(Object[] parameters)  
public Recordset execute(Object[] parameters, int options)  
public int executeUpdate(Object[] parameters)  
public int executeUpdate(Object[] parameters, int options)  
public int executeUpdate()  
```  
  
 **ExecuteUpdate**方法是特殊的案例方法，會使用特定參數來呼叫基礎 ADO **execute**方法。 **ExecuteUpdate**方法不支援傳回**記錄集**物件，因此會使用**AdoEnums.ExecuteOptions**修改**execute**方法的*options*參數。 **Execute**方法完成之後，其更新的*RecordsAffected*參數會傳回給**executeUpdate**方法，最後會以**int**傳回。  
  
### <a name="properties"></a>屬性  
  
```  
public com.ms.wfc.data.Connection getActiveConnection()  
public void setActiveConnection(com.ms.wfc.data.Connection con)  
public void setActiveConnection(String conString)  
public String getCommandText()  
public void setCommandText(String command)  
public int getCommandTimeout()  
public void setCommandTimeout(int timeout)  
public int getCommandType()  
public void setCommandType(int type)  
public String getName()  
public void setName(String name)  
public boolean getPrepared()  
public void setPrepared(boolean prepared)  
public int getState()  
public com.ms.wfc.data.Parameter getParameter(int n)  
public com.ms.wfc.data.Parameter getParameter(String n)  
public com.ms.wfc.data.Parameters getParameters()  
public AdoProperties getProperties()  
```  
  
## <a name="see-also"></a>另請參閱  
 [Command 物件 (ADO)](./command-object-ado.md)