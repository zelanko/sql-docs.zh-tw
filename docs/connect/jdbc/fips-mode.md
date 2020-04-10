---
title: JDBC 中的 FIPS 模式 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: efa536024021e1182ad565fe534d3e706f4e7eff
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80917953"
---
# <a name="fips-mode"></a>FIPS 模式

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver for SQL Server 支援在已設定為「符合 FIPS 140 規範」  的 JVM 中執行。

#### <a name="prerequisites"></a>Prerequisites

- 已設定 FIPS 的 JVM
- 適當的 SSL 憑證
- 適當的原則檔案
- 適當的設定參數

## <a name="fips-configured-jvm"></a>已設定 FIPS 的 JVM

一般來說，應用程式可以設定 `java.security` 檔案來使用符合 FIPS 規範的密碼編譯提供者。 請參閱您 JVM 的特定文件以了解如何設定 FIPS 140 合規性。

若要查看適用於 FIPS 設定的已核准模組，請參閱[密碼編譯模組驗證計畫中的已驗證模組](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules) \(英文\)。

廠商可能需要進行一些額外的步驟以搭配 FIPS 設定 JVM。

## <a name="appropriate-ssl-certificate"></a>適當的 SSL 憑證
若要在 FIPS 模式中連線到 SQL Server，需要有效的 SSL 憑證。 將其安裝或匯入到已啟用 FIPS 之用戶端電腦 (JVM) 的 Java Key Store 上。

### <a name="importing-ssl-certificate-in-java-keystore"></a>將 SSL 憑證匯入 Java KeyStore
針對 FIPS，您很可能需要以 PKCS 或提供者特定的格式來匯入憑證 (.cert)。
使用下列程式碼片段來匯入 SSL 憑證，並搭配適當的 KeyStore 格式將其儲存在工作目錄中。 _TRUST\_STORE\_PASSWORD_ 是您針對 Java KeyStore 的密碼。

```java
public void saveGenericKeyStore(
        String provider,
        String trustStoreType,
        String certName,
        String certPath
        ) throws KeyStoreException, CertificateException,
            NoSuchAlgorithmException, NoSuchProviderException,
            IOException
{
    KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
    FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
    ks.load(null, null);
    ks.setCertificateEntry(certName, getCertificate(certPath));
    ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
    os.flush();
    os.close();
}

private Certificate getCertificate(String pathName)
        throws FileNotFoundException, CertificateException
{
    FileInputStream fis = new FileInputStream(pathName);
    CertificateFactory cf = CertificateFactory.getInstance("X.509");
    return cf.generateCertificate(fis);
}
```

下列範例會搭配 BouncyCastle 提供者以 PKCS12 格式匯入 Azure SSL 憑證。 透過使用下列程式碼片段，可將該憑證匯入到名為 _MyTrustStore\_PKCS12_ 的工作目錄中：

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>適當的原則檔案
針對某些 FIPS 提供者，需要無限制的原則 jars。 在那種情況下，針對 Sun / Oracle，請下載適用於 [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) \(英文\) 或[ JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html) \(英文\) 的 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔。 

## <a name="appropriate-configuration-parameters"></a>適當的設定參數
若要在符合 FIPS 規範的模式中執行 JDBC 驅動程式，請依下表所示設定連線屬性。 

#### <a name="properties"></a>屬性 

|屬性|類型|預設|描述|注意|
|---|---|---|---|---|
|encrypt|boolean ["true / false"]|"false"|針對啟用 FIPS 的 JVM，加密屬性應該為 **true**||
|TrustServerCertificate|boolean ["true / false"]|"false"|針對 FIPS，使用者需要驗證憑證鏈結，因此使用者應該針對此屬性使用 **"false"** 值。 ||
|trustStore|String|null|您已匯入憑證的 Java KeyStore 檔案路徑。 如果您是在您的系統上安裝憑證，便不需要傳遞任何內容。 驅動程式會使用 cacerts 或 jssecacerts 檔案。||
|trustStorePassword|String|null|用於檢查 trustStore 資料完整性的密碼。||
|fips|boolean ["true / false"]|"false"|針對啟用 FIPS 的 JVM，此屬性應該為 **true**|已在 6.1.4 中新增 (穩定版本為 6.2.2)||
|fipsProvider|String|null|在 JVM 中設定的 FIPS 提供者。 例如，BCFIPS 或 SunPKCS11-NSS |已在 6.1.2 中新增 (穩定版本為 6.2.2)，已在 6.4.0 中淘汰。請參閱[這裡](https://github.com/Microsoft/mssql-jdbc/pull/460) \(英文\) 的詳細資料。|
|trustStoreType|String|JKS|針對 FIPS 模式，請將信任存放區類型設定為 PKCS12，或是由 FIPS 提供者所定義的類型 |已在 6.1.2 中新增 (穩定版本為 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
