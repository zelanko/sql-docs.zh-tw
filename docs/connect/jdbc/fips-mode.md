---
title: JDBC 中的 FIPS 模式 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
manager: kenvh
ms.openlocfilehash: 63681ee474d4993e248bf02dcabd9065317ffa39
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028060"
---
# <a name="fips-mode"></a>FIPS 模式

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

適用于 SQL Server 的 Microsoft JDBC Driver 支援在設定為*符合 FIPS 140 規範*的 jvm 中執行。

#### <a name="prerequisites"></a>Prerequisites

- FIPS 設定的 JVM
- 適當的 SSL 憑證
- 適當的原則檔案
- 適當的設定參數

## <a name="fips-configured-jvm"></a>FIPS 設定的 JVM

一般來說, 應用程式可以將`java.security`檔案設定成使用 FIPS 相容的加密提供者。 請參閱 JVM 的特定檔, 以瞭解如何設定 FIPS 140 合規性。

若要查看適用于 FIPS 設定的已核准模組, 請參閱[密碼編譯模組驗證程式中已驗證的模組](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules)。

廠商可能會有一些額外的步驟來設定具有 FIPS 的 JVM。

## <a name="appropriate-ssl-certificate"></a>適當的 SSL 憑證
若要連接到 FIPS 模式中的 SQL Server, 需要有效的 SSL 憑證。 在啟用 FIPS 的用戶端機器 (JVM) 上, 將它安裝或匯入到 JAVA 金鑰存放區。

### <a name="importing-ssl-certificate-in-java-keystore"></a>在 JAVA 金鑰儲存區中匯入 SSL 憑證
針對 FIPS, 您很可能需要以 PKCS 或提供者特定格式匯入憑證 (cert)。
使用下列程式碼片段來匯入 SSL 憑證, 並將它儲存在具有適當金鑰儲存區格式的工作目錄中。 TRUST STORE 密碼是您的 JAVA 金鑰_儲存區\_密碼。\__

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

下列範例會使用 BouncyCastle 提供者匯入 PKCS12 格式的 Azure SSL 憑證。 使用下列程式碼片段, 在名為_MyTrustStore\_PKCS12_的工作目錄中匯入憑證:

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>適當的原則檔案
對於某些 FIPS 提供者, 則需要不受限制的原則 jar。 在這種情況下, 對於 Sun/Oracle, 請下載適用于[JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)或[Jre 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)的 JAVA 密碼編譯延伸模組 (JCE) 無限制的強度區域原則檔案。 

## <a name="appropriate-configuration-parameters"></a>適當的設定參數
若要在 FIPS 相容模式中執行 JDBC 驅動程式, 請設定連接屬性, 如下表所示。 

#### <a name="properties"></a>屬性 

|屬性|類型|預設|描述|注意|
|---|---|---|---|---|
|encrypt|boolean ["true / false"]|"false"|針對啟用 FIPS 的 JVM, [加密] 屬性應為**true**||
|TrustServerCertificate|boolean ["true / false"]|"false"|針對 FIPS, 使用者必須驗證憑證鏈, 因此使用者應針對此屬性使用 **"false"** 值。 ||
|trustStore|String|null|您用來匯入憑證的 JAVA 金鑰儲存區檔案路徑。 如果您在系統上安裝憑證, 則不需要傳遞任何內容。 驅動程式會使用 cacerts 或 jssecacerts 檔案。||
|trustStorePassword|String|null|用於檢查 trustStore 資料完整性的密碼。||
|fips|boolean ["true / false"]|"false"|針對啟用 FIPS 的 JVM, 此屬性應為**true**|已在6.1.4 中新增 (穩定發行 6.2.2)||
|fipsProvider|String|null|在 JVM 中設定的 FIPS 提供者。 例如, BCFIPS 或 SunPKCS11-NSS |已在 6.1.2 (穩定發行 6.2.2) 中新增, 已在6.4.0 版中被取代-請參閱[這裡](https://github.com/Microsoft/mssql-jdbc/pull/460)的詳細資料。|
|trustStoreType|String|JKS|若為 FIPS 模式, 請設定信任存放區類型 PKCS12 或由 FIPS 提供者定義的類型 |已在6.1.2 中新增 (穩定發行 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
