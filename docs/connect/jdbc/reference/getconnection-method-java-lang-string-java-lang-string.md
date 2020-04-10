---
title: getConnection 方法 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c5dea8e183cb572bd0d70e9ccce01a203204b26c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925878"
---
# <a name="getconnection-method-javalangstring-javalangstring"></a>getConnection 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  嘗試與這個 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 物件所代表的資料來源建立連接，其方式是使用指定的使用者名稱和密碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Connection getConnection(java.lang.String username,  
                                         java.lang.String password)  
```  
  
#### <a name="parameters"></a>參數  
 *username*  
  
 包含使用者名稱的**字串**。  
  
 *password*  
  
 包含密碼的**字串**。  
  
## <a name="return-value"></a>傳回值  
 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 getConnection 方法是由 javax.sql.DataSource 介面中的 getConnection 方法所指定。  
  
 使用非 Null 使用者名稱或密碼呼叫 getConnection 方法時，將會取代初始化 SQLServerConnection 物件時，在 SQLServerDataSource 類別上所設定的使用者名稱與密碼屬性。 例如，如果呼叫者已經在資料來源上呼叫 [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) 和 [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)，然後呼叫 getConnection 並提供非 Null 使用者名稱或非 Null 密碼，則 setUser 和 setPassword 所設定之使用者名稱和密碼將會由傳遞給 getConnection 的使用者名稱和密碼取代。  
  
> [!NOTE]  
>  在此情況下，使用 [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md) 方法的呼叫在 URL 內設定的使用者名稱和密碼將不會變更。  
  
## <a name="see-also"></a>另請參閱  
 [getConnection 方法 &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
