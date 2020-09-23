---
description: setNCharacterStream 方法設定為 Reader 物件 - int
title: setNCharacterStream 方法設定為 Reader 物件 - int | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7732746b-eda5-469e-8567-e8546c4d81cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 74bcb32d53554b72f97c39ef17b480c428d8be92
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431650"
---
# <a name="setncharacterstream-method-int-javaioreader"></a>setNCharacterStream 方法 (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 Reader 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setNCharacterStream(int parameterIndex,  
                                                 java.io.Reader value)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterIndex*  
  
 指出參數索引的 **int**。  
  
 *value*  
  
 Reader 物件，其中包含參數值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setNCharacterStream 方法是由 java.sql.PreparedStatement 介面中的 setNCharacterStream 方法所指定。  
  
 此方法應該用於 **NCHAR**、**NVARCHAR**、**NTEXT** 和 **XML** 資料類型。  
  
## <a name="see-also"></a>另請參閱  
 [setNCharacterStream 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
