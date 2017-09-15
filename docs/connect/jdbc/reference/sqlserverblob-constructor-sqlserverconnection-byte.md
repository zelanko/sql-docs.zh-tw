---
title: "SQLServerBlob 建構函式 （SQLServerConnection，byte） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76b8fe0d719a2eb5f53fe20502d0cd3fe35ca6eb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverblob-constructor-sqlserverconnection-byte"></a>SQLServerBlob 建構函式 （SQLServerConnection，byte）
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  初始化的新執行個體[SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)類別時指定[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件和**位元組**陣列。  
  
> [!NOTE]  
>  這個方法在 JDBC Driver 2.0 版中已被取代。 請改用[createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md)方法[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)類別。  
  
## <a name="syntax"></a>語法  
  
```  
  
public SQLServerBlob(SQLServerConnection connection,  
                     byte[] data)  
```  
  
#### <a name="parameters"></a>參數  
 *連線*  
  
 
          SQLServerConnection 物件。  
  
 *資料*  
  
 A**位元組**陣列。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerBlob 建構函式](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [SQLServerBlob 成員](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 類別](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
