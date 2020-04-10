---
title: rowDeleted 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowDeleted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9c6db315-e614-4604-b020-41af6a214cc1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4f761f4780b2fdb5da210db5bfb38d2368d865f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80903904"
---
# <a name="rowdeleted-method-sqlserverresultset"></a>rowDeleted 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出資料列是否已遭刪除。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean rowDeleted()  
```  
  
## <a name="return-value"></a>傳回值  
 如果資料列已經刪除且偵測到刪除，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 rowDeleted 方法是由 java.sql.ResultSet 介面中的 rowDeleted 方法指定。  
  
 刪除的資料列可能會在結果集中留下可見的漏洞。 這個方法可用來偵測結果集中的漏洞。 傳回的值取決於這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件是否可以偵測到刪除。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會偵測所有可更新資料指標類型的資料列，雖然順向和動態資料指標的偵測作業屬於暫時性質。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
