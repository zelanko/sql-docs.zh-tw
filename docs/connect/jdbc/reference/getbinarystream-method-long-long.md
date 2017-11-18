---
title: "getBinaryStream 方法 (long，long) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 30bc8882-04b4-4efd-95e4-7d3a2a8c1d47
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d53bb0e01198d1c4ecb5c08068be4220a34b765c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getbinarystream-method-long-long"></a>getBinaryStream 方法 (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用指定的開始位置和長度，傳回包含部分 BLOB 值的輸入資料流物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.InputStream getBinaryStream(long pos, long length)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 這是要擷取之部分值中第一個位元組的位移。  
  
 *length*  
  
 這是要擷取之部分值中的位元組長度。  
  
## <a name="return-value"></a>傳回值  
 包含 BLOB 資料的輸入資料流。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetBinaryStream 方法 java.sql.Blob 介面中所指定此 getBinaryStream 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerBlob 方法](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob 成員](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 類別](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

