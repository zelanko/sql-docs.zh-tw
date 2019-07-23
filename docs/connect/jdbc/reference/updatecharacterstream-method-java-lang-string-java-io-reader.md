---
title: updateCharacterStream 方法 (java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8ec22a9-4bbd-4759-9f21-957304ef3a5e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5300c381b7b64e90cdd9d6a9d3555ffce6a9af52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996672"
---
# <a name="updatecharacterstream-method-javalangstring-javaioreader"></a>updateCharacterStream 方法 (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用字元資料流值，更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateCharacterStream(java.lang.String columnLabel,  
                                  java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 **String**，包含資料行標籤。  
  
 *reader*  
  
 Reader 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 updateCharacterStream 方法是由 sql-dmo 介面中的 updateCharacterStream 方法指定。  
  
 這個方法會透過 Reader 物件將 Unicode 字元傳遞到選取的文字和二進位資料行。 這包括所有的文字資料行，以及 **binary**、**varbinary**、**varbinary(max)** 、**image** 和 **xml** 等資料行，但是不包含 **udt** 資料行。  
  
 針對**image**、 **text**和**Ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料類型使用這個方法可能會影響效能。  
  
## <a name="see-also"></a>另請參閱  
 [updateCharacterStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
