---
title: setPortNumber 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 59c5fa23-bc1a-4142-af17-70e275f0b833
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e533001c334f9f448a39f31cbfc34ef93f46f08d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920764"
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
  
## <a name="remarks"></a>備註  
 通訊埠編號為 TCP/IP 通訊埠編號，當開啟與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之間的通訊端連線時就會使用此編號。 如果未設定 portNumber 屬性，[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md) 方法會傳回預設值 1433。  
  
> [!NOTE]  
>  setPortNumber 方法不會針對傳入的連接埠值進行任何範圍檢查。 您可以在不觸發錯誤的情況下傳遞無效的連接埠號碼，例如 99999。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
