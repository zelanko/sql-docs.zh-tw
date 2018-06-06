---
title: updateCharacterStream 方法 （int，java.io.Reader） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4dddf885-0482-4776-8e9a-69f6c6270931
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c24424c7c7f4183293871a39bb8eb04d72dacd05
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
  
 讀取器物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 UpdateCharacterStream 方法 java.sql.ResultSet 介面中所指定此 updateCharacterStream 方法。  
  
 這個方法會讀取器物件的 Unicode 字元傳遞到選取的文字和二進位資料行。 這包括所有的文字資料行和**二進位**， **varbinary**， **varbinary （max)**，**映像**，和**xml**資料行，但不是**udt**資料行。  
  
 使用這個方法來**映像**，**文字**，和**ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料型別可能會影響效能。  
  
## <a name="see-also"></a>另請參閱  
 [updateCharacterStream 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
