---
title: getSendStringParametersAsUnicode 方法 (SQLServerDataSource) |Microsoft 文件
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
- SQLServerDataSource.getSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3836d0ab-c3fb-41ff-bb89-10389594ae51
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 338343f56f765e33fe0a8d81e6284bc4e84cf564
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32837273"
---
# <a name="getsendstringparametersasunicode-method-sqlserverdatasource"></a>getSendStringParametersAsUnicode 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回**布林**值，指出是否啟用伺服器以 UNICODE 格式傳送字串參數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean getSendStringParametersAsUnicode()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果伺服器以 UNICODE 格式傳送字串參數。 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 如果 sendStringParametersAsUnicode 屬性設定為**true**，這是預設值、 字串參數到伺服器以 UNICODE 格式傳送。 如果 sendStringParametersAsUnicode 設定為**false**，string 參數傳送到伺服器以 ASCII/MBCS 格式而非 UNICODE。 如果 sendStringParametersAsUnicode 未設定，getsendstringparametersasunicode 就會傳回預設值的**true**。  
  
 如需有關 sendStringParametersAsUnicode 連接屬性的詳細資訊，請參閱[設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
