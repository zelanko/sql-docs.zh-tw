---
title: getEncrypt 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getEncrypt Method (SQLServerDataSource)
apilocation:
- getEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 1cdb12dd-6e6f-4bbd-8f5f-9e630f3ee2c9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 031c56f7389fef6afefd2e0b61e07117fce0b6d5
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924947"
---
# <a name="getencrypt-method-sqlserverdatasource"></a>getEncrypt 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回 **Boolean** 值，這個值會指出是否啟用 encrypt 屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean getEncypt()  
```  
  
## <a name="return-value"></a>傳回值  
 如果啟用 encrypt 屬性，則為 **true**， 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 如果 encrypt 屬性已設為 **true**，則 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 會確定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 將針對用戶端和伺服器之間傳送的所有資料使用 SSL 加密，條件是伺服器上必須先安裝憑證。  
  
 如果 encrypt 屬性未指定或設定為 **false**，驅動程式將不會強制 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援 SSL 加密。 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體未設定為強制 SSL 加密，這時不用任何加密就可以建立連線。 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體設定為強制 SSL 加密，則在正確設定的 Java 虛擬機器 (JVM) 上執行時，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 將會自動啟用 SSL 加密，否則連線會終止，且驅動程式會引發錯誤。 如果未設定 encryption 屬性，[getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md) 方法會傳回預設值 **false**。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
