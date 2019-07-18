---
title: setResponseBuffering 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: c9e43ff2-8117-4dca-982d-83c863d0c8e1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fa4e1c6921495448ce0a1e01a972b1786a69efd9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796754"
---
# <a name="setresponsebuffering-method-sqlserverdatasource"></a>setResponseBuffering 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定連線的回應緩衝模式，此連線是使用這個 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 物件所建立的。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>參數  
 *value*  
  
 **String**，包含緩衝和資料流模式。 有效模式可能是下列其中一個區分大小寫的 String：**full** 或 **adaptive**。  
  
## <a name="remarks"></a>Remarks  
 **full** 值會指定在執行階段從伺服器讀取整個結果。  
  
 **adaptive** 值會指定在必要時緩衝處理可能的資料下限。 **adaptive** 值是預設緩衝模式。  
  
 如需使用回應緩衝模式的詳細資訊，請參閱 <<c0> [ 使用適應性緩衝](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
