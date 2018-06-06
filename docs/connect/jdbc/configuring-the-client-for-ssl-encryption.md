---
title: 設定用戶端進行 SSL 加密 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ae34cd1f-3569-4759-80c7-7c9b33b3e9eb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c7a45a0da57be9df27d205b644e1d7156151982f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="configuring-the-client-for-ssl-encryption"></a>設定 SSL 加密的用戶端
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]或用戶端必須驗證伺服器為正確的伺服器，而且其憑證由用戶端所信任的憑證授權單位發行。 若要驗證伺服器憑證，必須在連接時間提供信任的資料。 此外，伺服器憑證的發行者必須是用戶端所信任的憑證授權單位。  
  
 本主題會先描述如何在用戶端電腦中提供信任的資料。 接著，本主題會描述如何在私人憑證授權單位發行 SQL Server 的安全通訊端層 (SSL) 憑證執行個體時，將伺服器憑證匯入到用戶端電腦的信任存放區中。  
  
 如需驗證伺服器憑證的詳細資訊，請參閱 < 驗證伺服器 SSL 憑證 」 一節[了解 SSL 支援](../../connect/jdbc/understanding-ssl-support.md)。  
  
## <a name="configuring-the-client-trust-store"></a>設定用戶端信任存放區  
 驗證伺服器憑證，必須在使用的連接時間提供信任的資料需要**trustStore**和**trustStorePassword**連接屬性明確地或隱含地使用基礎 Java Virtual Machine (JVM) 的預設信任存放區。 如需有關如何設定**trustStore**和**trustStorePassword**屬性在連接字串中，請參閱[使用 SSL 加密連接](../../connect/jdbc/connecting-with-ssl-encryption.md)。  
  
 如果**trustStore**屬性是未指定或設為 null，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]會依賴基礎 JVM 的安全性提供者，Java Secure Socket Extension (SunJSSE)。 SunJSSE 提供者會提供預設 TrustManager，用來驗證對信任的信任存放區中提供資料的 SQL Server 所傳回的 X.509 憑證。  
  
 TrustManager 會嘗試以下列搜尋順序找出預設的 trustStore:  
  
-   如果已定義系統屬性"javax.net.ssl.trustStore"，TrustManager 會嘗試尋找預設的 trustStore 檔案使用該系統屬性所指定的檔名。  
  
-   如果未指定"javax.net.ssl.trustStore"系統屬性，而且如果檔案 「\<java 首頁 >/lib/安全性/jssecacerts"存在，會使用該檔案。  
  
-   如果檔案 「\<java 首頁 >/lib/安全性/cacerts"存在，會使用該檔案。  
  
 如需詳細資訊，請參閱 Sun Microsystems 網站上的 SUNX509 TrustManager 介面文件。  
  
 Java Runtime Environment 可讓您設定 trustStore 和 trustStorePassword 系統屬性，如下所示：  
  
```  
java -Djavax.net.ssl.trustStore=C:\MyCertificates\storeName  
java -Djavax.net.ssl.trustStorePassword=storePassword  
```  
  
 在這個情況下，在此 JVM 上執行的任何應用程式都會使用這些設定做為預設值。 若要覆寫您的應用程式中的預設設定，您應該設定**trustStore**和**trustStorePassword**連接字串中或在適當的連接屬性setter 方法[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)類別。  
  
 此外，您可以設定和管理預設信任存放區檔案，例如"\<-h >/lib/安全性/jssecacerts"和"\<-h >/lib/安全性/cacerts"。 若要這樣做，請使用與 JRE (Java Runtime Environment) 一起安裝的 JAVA "keytool" 公用程式。 如需有關 "keytool" 公用程式的詳細資訊，請參閱 Sun Microsystems 網站上的 keytool 文件。  
  
### <a name="importing-the-server-certificate-to-trust-store"></a>將伺服器憑證匯入到信任存放區  
 在 SSL 交握期間，伺服器會將其公開金鑰憑證傳送到用戶端。 公開金鑰憑證的發行者也就是所謂的「憑證授權單位 (CA)」。 用戶端必須確保憑證授權單位為用戶端所信任的憑證授權單位。 事先知道信任之 CA 的公開金鑰即可達到這個目的。 一般而言，JVM 隨附一組預先定義之信任的憑證授權單位。  
  
 如果 SQL Server 的 SSL 憑證執行個體是由私人憑證授權單位發行，您必須在用戶端電腦的信任存放區中，將憑證授權單位的憑證加入到信任之憑證的清單中。  
  
 若要這樣做，請使用與 JRE (Java Runtime Environment) 一起安裝的 JAVA "keytool" 公用程式。 下列命令提示字元示範如何使用 "keytool" 公用程式，從檔案匯入憑證：  
  
```  
keytool -import -v -trustcacerts -alias myServer -file caCert.cer -keystore truststore.ks  
```  
  
 此範例使用名稱為 "caCert.cer" 的檔案當做憑證檔案。 您必須從伺服器取得此憑證檔案。 下列步驟說明如何將伺服器憑證匯出到檔案：  
  
1.  按一下 [開始]、[執行]，然後輸入 MMC  (MMC 是 Microsoft Management Console 的縮寫字)。  
  
2.  在 MMC 中，開啟 [憑證]。  
  
3.  展開 [個人]、[憑證]。  
  
4.  以滑鼠右鍵按一下伺服器憑證，然後選取 [所有工作]\[匯出]。  
  
5.  按 [下一步]，移出「憑證匯出精靈」的 [歡迎] 對話方塊。  
  
6.  確認選取 [否，不要匯出私密金鑰]，然後按 [下一步]。  
  
7.  請確認有選取 [DER 編碼二位元 X.509 (.CER)] 或 [Base-64 編碼 X.509 (.CER)]，然後按 [下一步]。  
  
8.  輸入匯出檔案名稱。  
  
9. 按 [下一步]，然後按一下 [完成]，即可匯出憑證。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)   
 [保護 JDBC Driver 應用程式](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
