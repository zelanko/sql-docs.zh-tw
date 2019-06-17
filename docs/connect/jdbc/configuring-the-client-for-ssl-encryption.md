---
title: 設定 SSL 加密的用戶端 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ae34cd1f-3569-4759-80c7-7c9b33b3e9eb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9f5ec4a56beb5595353671c0f2aab18bf30e5f87
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797466"
---
# <a name="configuring-the-client-for-ssl-encryption"></a>設定 SSL 加密的用戶端
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 或用戶端必須驗證伺服器為正確的伺服器而且其憑證是由用戶端所信任的憑證授權單位發行。 若要驗證伺服器憑證，必須在連接時間提供信任的資料。 此外，伺服器憑證的發行者必須是用戶端所信任的憑證授權單位。  
  
 本主題會先描述如何在用戶端電腦中提供信任的資料。 接著，本主題會描述如何在私人憑證授權單位發行 SQL Server 的安全通訊端層 (SSL) 憑證執行個體時，將伺服器憑證匯入到用戶端電腦的信任存放區中。  
  
 如需驗證伺服器憑證的詳細資訊，請參閱[了解 SSL 支援](../../connect/jdbc/understanding-ssl-support.md)中的＜驗證 Server SSL 憑證＞一節。  
  
## <a name="configuring-the-client-trust-store"></a>設定用戶端信任存放區  
 驗證伺服器憑證時，需要在連接時間明確地使用 **trustStore** 和 **trustStorePassword** 連接屬性，或隱含地使用基礎 Java Virtual Machine (JVM) 的預設信任存放區來提供信任的資料。 如需如何在連接字串中設定 **trustStore** 和 **trustStorePassword** 屬性的詳細資訊，請參閱[使用 SSL 加密連接](../../connect/jdbc/connecting-with-ssl-encryption.md)。  
  
 如果未指定 **trustStore** 屬性，或將其設定為 null，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 將會依賴基礎 JVM 的安全性提供者，也就是 Java Secure Socket Extension (SunJSSE)。 SunJSSE 提供者會提供預設的 TrustManager，用於驗證 SQL Server 根據信任存放區中所提供信任資料傳回的 X.509 憑證。  
  
 TrustManager 會嘗試以下列搜尋順序找出預設的 trustStore：  
  
-   如果有定義系統屬性 "javax.net.ssl.trustStore"，TrustManager 會嘗試使用該系統屬性所指定的檔案名稱，尋找預設的 trustStore 檔案。  
  
-   如果未指定 "javax.net.ssl.trustStore" 系統屬性，而且 "\<java-home>/lib/security/jssecacerts" 檔案存在，則會使用該檔案。  
  
-   如果 "\<java-home>/lib/security/cacerts" 檔案存在，則會使用該檔案。  
  
 如需詳細資訊，請參閱 Sun Microsystems 網站上的 SUNX509 TrustManager 介面文件。  
  
 Java Runtime Environment 可讓您設定 trustStore 和 trustStorePassword 系統屬性，如下所示：  
  
```  
java -Djavax.net.ssl.trustStore=C:\MyCertificates\storeName  
java -Djavax.net.ssl.trustStorePassword=storePassword  
```  
  
 在這個情況下，在此 JVM 上執行的任何應用程式都會使用這些設定做為預設值。 若要覆寫應用程式中的預設值，您應該在連接字串或 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 類別的適當 setter 方法中，設定 **trustStore** 和 **trustStorePassword** 連接屬性。  
  
 此外，您可以設定與管理預設的信任存放區檔案，例如 "\<java-home>/lib/security/jssecacerts" 和 "\<java-home>/lib/security/cacerts"。 若要這樣做，請使用與 JRE (Java Runtime Environment) 一起安裝的 JAVA "keytool" 公用程式。 如需有關 "keytool" 公用程式的詳細資訊，請參閱 Sun Microsystems 網站上的 keytool 文件。  
  
### <a name="importing-the-server-certificate-to-trust-store"></a>將伺服器憑證匯入到信任存放區  
 在 SSL 交握期間，伺服器會將其公開金鑰憑證傳送到用戶端。 公開金鑰憑證的發行者也就是所謂的「憑證授權單位 (CA)」。 用戶端必須確保憑證授權單位為用戶端所信任的憑證授權單位。 事先知道信任之 CA 的公開金鑰即可達到這個目的。 一般而言，JVM 隨附一組預先定義之信任的憑證授權單位。  
  
 如果 SQL Server 的 SSL 憑證執行個體是由私人憑證授權單位發行，您必須在用戶端電腦的信任存放區中，將憑證授權單位的憑證加入到信任之憑證的清單中。  
  
 若要這樣做，請使用與 JRE (Java Runtime Environment) 一起安裝的 JAVA "keytool" 公用程式。 下列命令提示字元示範如何使用 "keytool" 公用程式，從檔案匯入憑證：  
  
```  
keytool -import -v -trustcacerts -alias myServer -file caCert.cer -keystore truststore.ks  
```  
  
 此範例使用名稱為 "caCert.cer" 的檔案當做憑證檔案。 您必須從伺服器取得此憑證檔案。 下列步驟說明如何將伺服器憑證匯出到檔案：  
  
1.  按一下 [開始]、[執行]，然後輸入 MMC (MMC 是 Microsoft Management Console 的縮寫字)。  
  
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
  
  
