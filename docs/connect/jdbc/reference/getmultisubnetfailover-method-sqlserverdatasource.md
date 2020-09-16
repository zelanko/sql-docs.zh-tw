---
description: getMultiSubnetFailover 方法 (SQLServerDataSource)
title: getMultiSubnetFailover 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1e8cb175-5f4c-4208-b4f5-3646990a30e3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea1decabd2ed631249d894aaaf8b077c405036f5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435370"
---
# <a name="getmultisubnetfailover-method-sqlserverdatasource"></a>getMultiSubnetFailover 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回 **multiSubnetFailover** 連接屬性的值。  
  
## <a name="syntax"></a>語法  
  
```vb  
public boolean getMultiSubnetFailover();  
```  
  
## <a name="return-value"></a>傳回值  
 傳回 true 或 false (取決於連接屬性的目前設定)。  
  
## <a name="remarks"></a>備註  
 如需 **multiSubnetFailover** 連接屬性的詳細資訊，請參閱[設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource.setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)   
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
