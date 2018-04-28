---
title: setIntegratedSecurity 方法 (SQLServerDataSource) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDataSource.setIntegratedSecurity
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c968ee4-b041-424a-bf69-cc2c4a4f51c6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 320db4baa925a55039623180d092dd3845e0d691
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="setintegratedsecurity-method-sqlserverdatasource"></a>setIntegratedSecurity 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定**布林**值，指出是否啟用 integratedSecurity 屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setIntegratedSecurity(boolean enable)  
```  
  
#### <a name="parameters"></a>參數  
 *enable*  
  
 **true**如果已啟用 integratedsecurity 則。 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 設為"**true**」 表示會透過使用 Windows 認證[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]應用程式的使用者進行驗證。 如果 「**true**"，則[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]將搜尋本機電腦認證快取，在電腦或網路登入時已經提供的認證。 如果 「**false**」，必須提供使用者名稱和密碼。  
  
> [!NOTE]  
>  這個屬性才支援[!INCLUDE[msCoName](../../../includes/msconame_md.md)]Windows 作業系統。  
  
 如需有關如何使用整合式的驗證的詳細資訊，請參閱[建立連接 URL](../../../connect/jdbc/building-the-connection-url.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
