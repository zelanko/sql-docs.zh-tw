---
title: setPacketSize 方法 (SQLServerDataSource) |Microsoft Docs
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
- SQLServerDataSource.setPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5d490edc-a223-4870-a838-784952497e5f
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c99c8516c6e38400798921aeae01f2387066e228
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785446"
---
# <a name="setpacketsize-method-sqlserverdatasource"></a>setPacketSize 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定用來與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通訊的目前網路封包大小 (以位元組指定)。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setPacketSize(int packetSize)  
```  
  
#### <a name="parameters"></a>參數  
 *packetSize*  
  
 包含網路封包大小的 **int** 值。  
  
## <a name="remarks"></a>Remarks  
 這個屬性的可接受值範圍是 [-1 | 0 | 512..32767]。 如果將此屬性設為可接受範圍以外的值，將發生例外狀況。  
  
 應用程式可能希望在透過 SSL (Secure Sockets Layer) 加密連線時設定 packetSize 屬性。 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 會與伺服器交涉封包大小。 如果 encrypt 屬性設定為 "**true**"，而交涉後的封包大小大於 Java 虛擬機器 (JVM) 預設安全性提供者的 SSL 記錄大小，則驅動程式將會引發錯誤，並終止連線。  
  
 此外，應用程式可能希望在未要求 SSL 加密情況下設定 packetSize 屬性。 在這種情況下，如果伺服器要求用戶端支援 SSL 加密，則驅動程式就會檢查 JVM 之預設安全性提供者的 SSL 記錄大小。 如果 packetSize 屬性大於 JVM 之預設安全性提供者的 SSL 記錄大小，則驅動程式將引發錯誤，並終止連接。  
  
 如需使用 SSL 的詳細資訊，請參閱[Using SSL Encryption](../../../connect/jdbc/using-ssl-encryption.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
