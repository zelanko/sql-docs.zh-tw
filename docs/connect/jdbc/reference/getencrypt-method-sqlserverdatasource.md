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
ms.openlocfilehash: 7edee23f7111b55a6d34ac6ae10bf3720879fc01
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219291"
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
 如果 encrypt 屬性已設為 **true**，則 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 會確保 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 將針對用戶端和伺服器之間傳送的所有資料使用 TLS 加密，條件是伺服器上必須先安裝憑證。  
  
 如果 encrypt 屬性未指定或設定為 **false**，則驅動程式將不會強制 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援 TLS 加密。 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體未設定為強制 TLS 加密，則不使用任何加密即可建立連線。 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體設定為強制 TLS 加密，則在正確設定的 JAVA 虛擬機器 (JVM) 上執行時，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 將會自動啟用 TLS 加密，否則連線會中止，且驅動程式會引發錯誤。 如果未設定 encryption 屬性，[getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md) 方法會傳回預設值 **false**。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
