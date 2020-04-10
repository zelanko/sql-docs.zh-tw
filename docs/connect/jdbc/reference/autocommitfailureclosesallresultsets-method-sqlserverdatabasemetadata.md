---
title: JDBC 驅動程式是否會關閉開啟的結果集 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1739ecb5-e5cb-4807-b5a8-97c0299929d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9d76ebdcd4eac2fca67d04693aa2fe24fa279da
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927984"
---
# <a name="autocommitfailureclosesallresultsets-method-sqlserverdatabasemetadata"></a>autoCommitFailureClosesAllResultSets 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出當自動認可啟用且擲出例外狀況時，JDBC Driver 是否會關閉所有開啟的結果集，包括可保留資料的結果集。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean autoCommitFailureClosesAllResultSets()  
```  
  
## <a name="return-value"></a>傳回值  
 如果在自動認可已啟用且擲出例外狀況情況下會關閉所有開啟的結果集 (包括可保留資料的結果集)，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 autoCommitFailureClosesAllResultSets 方法是由 java.sql.DatabaseMetaData 介面中的 autoCommitFailureClosesAllResultSets 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
