---
title: SQLServerBlob 建構函式 （SQLServerConnection，byte） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d93e5bee03976c5ae9c55247f98ba180e237a4e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32847033"
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
  
 *data*  
  
 A**位元組**陣列。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerBlob 建構函式](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [SQLServerBlob 成員](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 類別](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
