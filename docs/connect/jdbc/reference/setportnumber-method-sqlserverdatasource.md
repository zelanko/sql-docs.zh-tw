---
title: setPortNumber 方法 (SQLServerDataSource) |Microsoft Docs
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
- SQLServerDataSource.setPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 59c5fa23-bc1a-4142-af17-70e275f0b833
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 608c83e843941f80d4f6c9805711394975fb0c20
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784194"
---
# <a name="setportnumber-method-sqlserverdatasource"></a>setPortNumber 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定用來與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通訊的連接埠號碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setPortNumber(int portNumber)  
```  
  
#### <a name="parameters"></a>參數  
 *portNumber*  
  
 包含連接埠號碼 **int** 值。  
  
## <a name="remarks"></a>Remarks  
 連接埠號碼為 TCP/IP 連接埠號碼，當開啟與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之間的通訊端連線時就會使用它。 如果未設定 portNumber 屬性，[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md) 方法會傳回預設值 1433。  
  
> [!NOTE]  
>  SetPortNumber 方法不會執行任何範圍檢查傳入的連接埠值。 您可以傳遞無效，如 99999，而不觸發錯誤的連接埠號碼。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
