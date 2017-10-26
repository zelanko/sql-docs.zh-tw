---
title: "setPacketSize 方法 (SQLServerDataSource) |Microsoft 文件"
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
- SQLServerDataSource.setPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9684140ed084cc7a096675935ceec81209f8fa66
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setpacketsize-method-sqlserverdatasource"></a>setPacketSize 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定用來與通訊的目前網路封包大小[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，以位元組為單位指定。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>參數  
 *封包*  
  
 **Int**值，其中包含網路封包大小。  
  
## <a name="remarks"></a>備註  
 這個屬性的可接受值範圍是 [-1 | 0 | 512..32767]。 如果將此屬性設為可接受範圍以外的值，將發生例外狀況。  
  
 應用程式可能希望在透過 SSL (Secure Sockets Layer) 加密連線時設定 packetSize 屬性。 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]交涉與伺服器的封包大小。 如果 encrypt 屬性設定為"**true**」 並交涉封包大小大於 Java Virtual Machine (JVM) 的預設安全性提供者的 SSL 記錄大小，驅動程式將會引發錯誤，並終止連接。  
  
 此外，應用程式可能希望在未要求 SSL 加密情況下設定 packetSize 屬性。 在這種情況下，如果伺服器要求用戶端支援 SSL 加密，則驅動程式就會檢查 JVM 之預設安全性提供者的 SSL 記錄大小。 如果 packetSize 屬性大於 JVM 之預設安全性提供者的 SSL 記錄大小，則驅動程式將引發錯誤，並終止連接。  
  
 如需有關使用 SSL 的詳細資訊，請參閱[使用 SSL 加密](../../../connect/jdbc/using-ssl-encryption.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

