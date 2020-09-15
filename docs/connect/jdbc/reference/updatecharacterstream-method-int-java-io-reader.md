---
description: updateCharacterStream 方法 (int, java.io.Reader)
title: updateCharacterStream 文件 (int, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4dddf885-0482-4776-8e9a-69f6c6270931
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8f4d8d4ae626fada30b9dacda009ddfe5a2553fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354014"
---
# <a name="updatecharacterstream-method-int-javaioreader"></a>updateCharacterStream 方法 (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用字元資料流值，更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
 *x*  
  
 Reader 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 updateCharacterStream 方法是由 java.sql.ResultSet 介面中的 updateCharacterStream 方法所指定。  
  
 這個方法會透過 Reader 物件將 Unicode 字元傳遞到選取的文字和二進位資料行。 這包括所有的文字資料行，以及 **binary**、**varbinary**、**varbinary(max)** 、**image** 和 **xml** 等資料行，但是不包含 **udt** 資料行。  
  
 將這個方法用於 **image**、**text** 和 **ntext**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型可能會影響效能。  
  
## <a name="see-also"></a>另請參閱  
 [updateCharacterStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
