---
title: getResponseBuffering 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getResponseBuffering()
apilocation:
- SQLServerDataSource.getResponseBuffering()
apitype: Assembly
ms.assetid: 19585a93-88a4-415e-a20e-12ba58cddeaa
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7ea9552ff9a9bf8d0a591f35670ca7147c67e18d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801355"
---
# <a name="getresponsebuffering-method-sqlserverdatasource"></a>getResponseBuffering 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回這個 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 物件的回應緩衝模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>傳回值  
 A**字串**可包含小寫**完整**或是**調適性**。  
  
## <a name="remarks"></a>Remarks  
 **full** 值會指定在執行階段從伺服器讀取整個結果。  
  
 **adaptive** 值會指定在必要時緩衝處理可能的資料下限。 **adaptive** 值是預設緩衝模式。  
  
 如需使用回應緩衝模式的詳細資訊，請參閱 <<c0> [ 使用適應性緩衝](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
## <a name="see-also"></a>另請參閱  
 [setResponseBuffering 方法 &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)   
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
