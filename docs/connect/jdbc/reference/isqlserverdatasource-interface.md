---
title: "ISQLServerDataSource 介面 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1d3242-19ca-4321-83fe-867a4f69f1d4
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 175e14fbd67d63080a0615d67fd5bf5123612b99
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="isqlserverdatasource-interface"></a>ISQLServerDataSource 介面
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立此物件代表之資料來源連接的 Factory。 此介面已加入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC 驅動程式 3.0。  
  
 **封裝：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** java.sql.CommonDataSource  
  
## <a name="syntax"></a>語法  
  
```  
  
public interface ISQLServerDataSource  
```  
  
## <a name="remarks"></a>備註  
 這個介面由實作[SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)。  
  
 這個介面會公開下列[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-特有的方法：  
  
|方法|如需詳細資訊，請參閱|  
|------------|-------------------------------|  
|public String getApplicationName()|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|  
|public String getDatabaseName()|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|  
|public String getDescription()|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|  
|public boolean getEncrypt()|[getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md)|  
|public String getFailoverPartner()|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|  
|public String getHostNameInCertificate()|[getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md)|  
|public String getInstanceName()|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|  
|public boolean getLastUpdateCount()|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|  
|public int getLockTimeout()|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|  
|public boolean getMultiSubnetFailover()|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|  
|public int getPacketSize()|[getPacketSize](../../../connect/jdbc/reference/getpacketsize-method-sqlserverdatasource.md)|  
|public int getPortNumber()|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|  
|public String getResponseBuffering()|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverdatasource.md)|  
|public String getSelectMethod()|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|  
|public boolean getSendStringParametersAsUnicode()|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|  
|public boolean getSendTimeAsDatetime()|[getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|  
|public String getServerName()|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|  
|public boolean getTrustServerCertificate()|[getTrustServerCertificate](../../../connect/jdbc/reference/gettrustservercertificate-method-sqlserverdatasource.md)|  
|public String getTrustStore()|[getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md)|  
|public String getURL()|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|  
|public String getUser()|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|  
|public String getWorkstationID()|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|  
|public boolean getXopenStates()|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|  
|public void setApplicationName(String)|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|  
|public void setAuthenticationSceme(String)|[setAuthenticationSceme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|  
|public void setDatabaseName(String)|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|  
|public void setDescription(String)|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|  
|public void setEncrypt(boolean)|[setEncrypt](../../../connect/jdbc/reference/setencrypt-method-sqlserverdatasource.md)|  
|public void setFailoverPartner(String)|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|  
|public void setHostNameInCertificate(String)|[setHostNameInCertificate](../../../connect/jdbc/reference/sethostnameincertificate-method-sqlserverdatasource.md)|  
|public void setInstanceName(String)|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|  
|public void setIntegratedSecurity(boolean)|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|  
|public void setLastUpdateCount(boolean)|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|  
|public void setLockTimeout(int)|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|  
|public void setMultiSubnetFailover(boolean multiSubnetFailover)|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|  
|public void setPacketSize(int)|[setPacketSize](../../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md)|  
|public void setPassword(String)|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|  
|public void setPortNumber(int)|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|  
|public void setResponseBuffering(String)|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)|  
|public void setSelectMethod(String)|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|  
|public void setSendStringParametersAsUnicode(boolean)|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|  
|public void setSendTimeAsDatetime(boolean)|[setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)|  
|public void setServerName(String)|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|  
|public void setTrustServerCertificate(boolean)|[setTrustServerCertificate](../../../connect/jdbc/reference/settrustservercertificate-method-sqlserverdatasource.md)|  
|public void setTrustStore(String)|[setTrustStore](../../../connect/jdbc/reference/settruststore-method-sqlserverdatasource.md)|  
|public void setTrustStorePassword(String)|[setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)|  
|public void setURL(String url)|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|  
|public void setUser(String)|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|  
|public void setWorkstationID(String)|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|  
|public void setXopenStates(boolean)|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
