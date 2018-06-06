---
title: 了解 SSL 支援 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 073f3b9e-8edd-4815-88ea-de0655d0325e
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 089ec1a4a16f9a0568bda9aa584948fd4704ae5f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-ssl-support"></a>了解 SSL 支援
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  當連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，如果應用程式要求加密而且的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]已設定為支援 SSL 加密，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]會起始 SSL 交握。 交握可讓伺服器與用戶端交涉要用來保護資料的加密和密碼編譯演算法。 SSL 交握完成後，用戶端和伺服器就可以安全地傳送加密的資料。 在 SSL 交握期間，伺服器會將其公開金鑰憑證傳送到用戶端。 公開金鑰憑證的發行者也就是所謂的「憑證授權單位 (CA)」。 用戶端負責驗證憑證授權單位為用戶端所信任的憑證授權單位。  
  
 如果應用程式沒有要求加密，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]將不會強制[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]支援 SSL 加密。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體未設定為強制 SSL 加密，而且不會加密連接。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體設定為強制 SSL 加密，驅動程式會自動啟用 SSL 加密時已正確設定 Java Virtual Machine (JVM) 上執行，或其他的連線已終止和驅動程式會引發錯誤。  
  
> [!NOTE]  
>  請確定傳遞給的值**serverName**完全相符的一般名稱 (CN) 或 DNS 名稱中主旨替代名稱 (SAN) SSL 連接的伺服器憑證中才會成功。  
  
> [!NOTE]  
>  如需有關如何設定 SSL 的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請參閱 < 加密的連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中的主題[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="remarks"></a>備註  
 為了允許應用程式使用 SSL 加密[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]導入了下列連接屬性從 1.2 版開始：**加密**， **trustServerCertificate**， **trustStore**， **trustStorePassword**，和**hostNameInCertificate**。 如需詳細資訊，請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 下表摘要說明如何[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]版本針對可能的 SSL 連接狀況運作。 每個狀況都使用一組不同的 SSL 連接屬性。 此資料表包括：  
  
-   **空白**: 「 屬性不存在的連接字串中 」  
  
-   **值**: 「 屬性存在於連接字串，而且其值有效 」  
  
-   **任何**:"並不重要的內容存在於連接字串，或其值是否有效 」  
  
> [!NOTE]  
>  相同的行為也適用於[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]使用者驗證與 Windows 整合式的驗證。  
  
|encrypt|trustServerCertificate|hostNameInCertificate|trustStore|trustStorePassword|行為|  
|-------------|----------------------------|---------------------------|----------------|------------------------|--------------|  
|false 或空白|任意|任意|任意|任意|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]將不會強制[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]支援 SSL 加密。 如果伺服器有自我簽署憑證，驅動程式會起始 SSL 憑證交換。 SSL 憑證將不會經過驗證，而且只有認證 (在登入封包中) 會經過加密。<br /><br /> 如果伺服器需要用戶端支援 SSL 加密，驅動程式將會起始 SSL 憑證交換。 SSL 憑證將不會經過驗證，但是整個通訊將會經過加密。|  
|true|true|任意|任意|任意|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]要求使用 SSL 加密[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。 請注意，如果**trustServerCertificate**屬性設定為"true"，驅動程式將不會驗證 SSL 憑證。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。|  
|true|false 或空白|空白|空白|空白|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]要求使用 SSL 加密[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式會使用**serverName**驗證伺服器 SSL 憑證，並依賴信任管理員 factory 的查閱規則，以決定要使用的憑證存放區在連接 URL 上指定的屬性。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。|  
|true|false 或空白|value|空白|空白|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]要求使用 SSL 加密[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式會使用指定的值來驗證 SSL 憑證的主體值**hostNameInCertificate**屬性。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。|  
|true|false 或空白|空白|value|value|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]要求使用 SSL 加密[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式會使用**trustStore**要尋找憑證 trustStore 檔案的屬性值和**trustStorePassword**屬性值，以檢查 trustStore 檔的完整性。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。|  
|true|false 或空白|空白|空白|value|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]要求使用 SSL 加密[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式會使用**trustStorePassword**屬性值，以檢查預設 trustStore 檔的完整性。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。|  
|true|false 或空白|空白|value|空白|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]要求使用 SSL 加密[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式會使用**trustStore**屬性值來查閱 trustStore 檔的位置。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。|  
|true|false 或空白|value|空白|value|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]要求使用 SSL 加密[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式會使用**trustStorePassword**屬性值，以檢查預設 trustStore 檔的完整性。 此外，驅動程式會使用**hostNameInCertificate**屬性值來驗證 SSL 憑證。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。|  
|true|false 或空白|value|value|空白|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]要求使用 SSL 加密[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式會使用**trustStore**屬性值來查閱 trustStore 檔的位置。 此外，驅動程式會使用**hostNameInCertificate**屬性值來驗證 SSL 憑證。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。|  
|true|false 或空白|value|value|value|[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]要求使用 SSL 加密[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式會使用**trustStore**要尋找憑證 trustStore 檔案的屬性值和**trustStorePassword**屬性值，以檢查 trustStore 檔的完整性。 此外，驅動程式會使用**hostNameInCertificate**屬性值來驗證 SSL 憑證。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。|  
  
 如果 encrypt 屬性設定為**true**、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]使用 JVM 的預設 JSSE 安全性提供者與交涉 SSL 加密[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 預設的安全性提供者可能不支援成功交涉 SSL 加密所需的所有功能。 例如，預設安全性提供者可能不支援的大小之 RSA 公開金鑰用於[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 憑證。 在此情況下，預設的安全性提供者可能會引發錯誤，造成 JDBC 驅動程式中止連接。 若要解決這個問題，請執行下列其中之一：  
  
-   設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的較小的 RSA 公開金鑰的伺服器憑證  
  
-   設定要使用不同的 JSSE 安全性提供者，在 JVM"\<java 首頁 > / lib/security/java.security"安全性屬性檔  
  
-   使用不同的 JVM  
  
## <a name="validating-server-ssl-certificate"></a>驗證 Server SSL 憑證  
 在 SSL 交握期間，伺服器會將其公開金鑰憑證傳送到用戶端。 JDBC 驅動程式或用戶端必須驗證伺服器憑證是由用戶端所信任的憑證授權單位發行。 驅動程式會要求伺服器憑證必須符合下列條件：  
  
-   憑證由信任的憑證授權單位所發行。  
  
-   憑證必須針對伺服器驗證而發行。  
  
-   憑證未過期。  
  
-   一般名稱 (CN) 在主旨或 DNS 名稱中主旨替代名稱 (SAN) 憑證的完全符合**serverName**連接字串中指定的值，若指定，則**hostNameInCertificate**屬性值。  
  
-   DNS 名稱可包含萬用字元。 但[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]不支援萬用字元比對。 也就是說，abc.com 不會符合 *.com 但是\*.com 會比對\*。 com。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)   
 [保護 JDBC Driver 應用程式](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
