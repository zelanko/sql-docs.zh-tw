---
title: getPacketSize 方法 (SQLServerDataSource) |Microsoft Docs
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
- SQLServerDataSource.getPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2e9f01a-2e51-47e5-90bf-43c62d1be74d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7067b0a96fdde31afdd8d4a4f67c757346385b5
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42787167"
---
# <a name="getpacketsize-method-sqlserverdatasource"></a>getPacketSize 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回用來與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通訊的目前網路封包大小 (以位元組為單位)。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getPacketSize()  
```  
  
## <a name="return-value"></a>傳回值  
 **int** 值，包含目前網路封包大小。  
  
## <a name="remarks"></a>Remarks  
 如果未設定 packetSize 屬性，getPacketSize 方法會傳回預設值 8000。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
