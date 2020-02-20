---
title: getTrustStore 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustStore Method (SQLServerDataSource)
apilocation:
- getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f35a71cc741411f3aad3408d366f3f70218fecdf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67978518"
---
# <a name="gettruststore-method-sqlserverdatasource"></a>getTrustStore 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回憑證 trustStore 檔案的路徑 (包括檔案名稱)。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>傳回值  
 **String**，其中包含憑證 trustStore 檔案的路徑 (包括檔案名稱)，如果未設定任何值則為 null。  
  
## <a name="remarks"></a>備註  
 如果未設定 trustStore 屬性，[getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md) 方法會傳回 null。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
