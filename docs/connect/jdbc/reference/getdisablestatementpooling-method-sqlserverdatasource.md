---
title: getDisableStatementPooling 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e250d21fe2b8b9cd46a15989ff1178c5512cb81
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80917593"
---
# <a name="getdisablestatementpooling-method-sqlserverdatasource"></a>getDisableStatementPooling 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回 **disableStatementPooling** 連接屬性的值。 此設定能控制陳述式共用是否已針對此連線啟用。

  
## <a name="syntax"></a>語法  
  
```
public boolean getDisableStatementPooling();  
```  
  
## <a name="return-value"></a>傳回值  
 **布林值**，其中包含 **disableStatementPooling** 連接屬性的值。
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>備註  
 從 JDBC 驅動程式 6.4 版開始，可以使用此方法。
 
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
