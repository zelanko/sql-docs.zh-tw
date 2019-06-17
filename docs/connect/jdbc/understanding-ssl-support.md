---
title: 了解 SSL 支援 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 073f3b9e-8edd-4815-88ea-de0655d0325e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fe0ef2f88f2db6035bce1e7e72fd216882964e82
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788437"
---
# <a name="understanding-ssl-support"></a>了解 SSL 支援

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，如果應用程式要求加密而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體設定為支援 SSL 加密，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會起始 SSL 交握。 交握可讓伺服器與用戶端交涉要用來保護資料的加密和密碼編譯演算法。 SSL 交握完成後，用戶端和伺服器就可以安全地傳送加密的資料。 在 SSL 交握期間，伺服器會將其公開金鑰憑證傳送到用戶端。 公開金鑰憑證的發行者也就是所謂的「憑證授權單位 (CA)」。 用戶端負責驗證憑證授權單位為用戶端所信任的憑證授權單位。  
  
如果應用程式沒有要求加密，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 將不會強制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 SSL 加密。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體未設定成強制 SSL 加密，這時不用加密就可以建立連線。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體設定為強制 SSL 加密，則在正確設定的 Java Virtual Machine (JVM) 上執行時，此驅動程式將會自動啟用 SSL 加密，否則連線會中止，而且驅動程式會引發錯誤。  
  
> [!NOTE]  
> 確定傳遞給 **serverName** 的值完全符合伺服器憑證中主旨替代名稱 (SAN) 內的一般名稱 (CN) 或 DNS 名稱，SSL 連線才會成功。  
>
> 如需如何針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定 SSL 的詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書中的＜加密 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連線＞主題。  
  
## <a name="remarks"></a>Remarks

為了讓應用程式能夠使用 SSL 加密，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 已從 1.2 版起引入下列連線屬性：**encrypt**、**trustServerCertificate**、**trustStore**、**trustStorePassword** 和 **hostNameInCertificate**。 如需詳細資訊，請參閱[設定連線屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 下表摘要說明 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 版本如何針對可能的 SSL 連線狀況運作。 每個狀況都使用一組不同的 SSL 連接屬性。 此資料表包括：  
  
- **空白**：「屬性不存在於連接字串中」  
  
- **值**：「屬性存在於連接字串中，而且其值有效」  
  
- **任意**：「屬性是否存在於連接字串中，或者其值是否有效都不重要」  
  
> [!NOTE]  
> 相同的行為也適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者驗證與 Windows 整合式驗證。  
  
| encrypt        | trustServerCertificate | hostNameInCertificate | trustStore | trustStorePassword | 行為                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------- | ---------------------- | --------------------- | ---------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| false 或空白 | 任意                    | 任意                   | 任意        | 任意                | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 將不會強制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 SSL 加密。 如果伺服器有自我簽署憑證，驅動程式會起始 SSL 憑證交換。 SSL 憑證將不會經過驗證，而且只有認證 (在登入封包中) 會經過加密。<br /><br /> 如果伺服器需要用戶端支援 SSL 加密，驅動程式將會起始 SSL 憑證交換。 SSL 憑證將不會經過驗證，但是整個通訊將會經過加密。                                                                                                                                                                                    |
| true           | true                   | 任意                   | 任意        | 任意                | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 要求搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 SSL 加密。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。 請注意，如果 **trustServerCertificate** 屬性設定為 "true"，驅動程式將不會驗證 SSL 憑證。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。                                                                                                                                                                                          |
| true           | false 或空白         | 空白                 | 空白      | 空白              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 要求搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 SSL 加密。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式將使用在連線 URL 上指定的 **serverName** 屬性，驗證伺服器 SSL 憑證，並依賴信任管理員 Factory 的查閱規則來決定要使用的憑證存放區。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。                                                                             |
| true           | false 或空白         | value                 | 空白      | 空白              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 要求搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 SSL 加密。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式將會使用針對 **hostNameInCertificate** 屬性指定的值，驗證 SSL 憑證的主旨值。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。                                                                                                                                                                 |
| true           | false 或空白         | 空白                 | value      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 要求搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 SSL 加密。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式將會使用 **trustStore** 屬性值來尋找憑證 trustStore 檔案與 **trustStorePassword** 屬性值以檢查 trustStore 檔案的完整性。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。                                                                                                                |
| true           | false 或空白         | 空白                 | 空白      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 要求搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 SSL 加密。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式將會使用 **trustStorePassword** 屬性值來檢查預設 trustStore 檔案的完整性。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。                                                                                                                                                                                  |
| true           | false 或空白         | 空白                 | value      | 空白              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 要求搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 SSL 加密。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式將會使用 **trustStore** 屬性值來查閱 trustStore 檔案的位置。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。                                                                                                                                                                                                 |
| true           | false 或空白         | value                 | 空白      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 要求搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 SSL 加密。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式將會使用 **trustStorePassword** 屬性值來檢查預設 trustStore 檔案的完整性。 此外，驅動程式將會使用 **hostNameInCertificate** 屬性值來驗證 SSL 憑證。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。                                                                   |
| true           | false 或空白         | value                 | value      | 空白              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 要求搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 SSL 加密。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式將會使用 **trustStore** 屬性值來查閱 trustStore 檔案的位置。 此外，驅動程式將會使用 **hostNameInCertificate** 屬性值來驗證 SSL 憑證。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。                                                                                  |
| true           | false 或空白         | value                 | value      | value              | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 要求搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 SSL 加密。<br /><br /> 如果伺服器要求用戶端支援 SSL 加密，或者，如果伺服器支援加密，驅動程式將會起始 SSL 憑證交換。<br /><br /> 驅動程式將會使用 **trustStore** 屬性值來尋找憑證 trustStore 檔案與 **trustStorePassword** 屬性值以檢查 trustStore 檔案的完整性。 此外，驅動程式將會使用 **hostNameInCertificate** 屬性值來驗證 SSL 憑證。<br /><br /> 如果伺服器的設定不支援加密，驅動程式將引發錯誤，並中止連接。 |
  
如果 encrypt 屬性設定為 **true**，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會使用 JVM 的預設 JSSE 安全性提供者與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交涉 SSL 加密。 預設的安全性提供者可能不支援成功交涉 SSL 加密所需的所有功能。 例如，預設的安全性提供者可能不支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSL 憑證中使用之 RSA 公開金鑰的大小。 在此情況下，預設的安全性提供者可能會引發錯誤，造成 JDBC 驅動程式中止連接。 若要解決這個問題，請執行下列其中之一：  
  
- 使用具有較小 RSA 公開金鑰的伺服器憑證設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
- 設定 JVM 在 "\<Java 主目錄>/lib/security/java.security" 安全性屬性檔中使用不同的 JSSE 安全性提供者  
  
- 使用不同的 JVM  
  
## <a name="validating-server-ssl-certificate"></a>驗證 Server SSL 憑證  

在 SSL 交握期間，伺服器會將其公開金鑰憑證傳送到用戶端。 JDBC 驅動程式或用戶端必須驗證伺服器憑證是由用戶端所信任的憑證授權單位發行。 驅動程式會要求伺服器憑證必須符合下列條件：  
  
- 憑證由信任的憑證授權單位所發行。  
  
- 憑證必須針對伺服器驗證而發行。  
  
- 憑證未過期。  
  
- 憑證之主旨內的一般名稱 (CN) 或是主旨替代名稱 (SAN) 內的 DNS 名稱會完全符合連接字串內所指定的 **serverName** 值或是 **hostNameInCertificate** 屬性值 (如果指定的話)。  
  
- DNS 名稱可包含萬用字元。 但是 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 不支援萬用字元比對。 也就是說，abc.com 不會符合 \*.com；但是 \*.com 會符合 \*.com。  
  
## <a name="see-also"></a>另請參閱

[使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)

[保護 JDBC Driver 應用程式](../../connect/jdbc/securing-jdbc-driver-applications.md)  
