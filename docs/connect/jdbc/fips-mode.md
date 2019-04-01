---
title: 在 JDBC 的 FIPS 模式 |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: craigg
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: kenvh
ms.openlocfilehash: 8fb6ea7bf6abfb1f347d0541a01bae91aacf5f1c
ms.sourcegitcommit: 0c049c539ae86264617672936b31d89456d63bb0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2019
ms.locfileid: "58618275"
---
# <a name="fips-mode"></a>FIPS 模式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver for SQL Server 支援在執行中設定的 Jvm *FIPS 140 相容*。

#### <a name="prerequisites"></a>Prerequisites

- FIPS 設定 JVM
- 適當的 SSL 憑證
- 適當的原則檔案
- 適當的組態參數

## <a name="fips-configured-jvm"></a>FIPS 設定 JVM

一般而言，應用程式可以設定`java.security`使用 FIPS 相容的密碼編譯提供者的檔案。 請參閱您的 JVM，如何設定 FIPS 140 合規性的專屬文件。

若要查看 FIPS 設定的已核准的模組，請參閱[密碼編譯模組驗證程式中的驗證模組](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules)。

供應商可能有一些額外步驟以設定 fips 的 JVM。

## <a name="appropriate-ssl-certificate"></a>適當的 SSL 憑證
若要連接到 SQL Server 在 FIPS 模式中，有效的 SSL 憑證則是必要項目。 安裝或匯入它 Java 金鑰存放區用戶端機器 (JVM) 上都啟用 FIPS。

### <a name="importing-ssl-certificate-in-java-keystore"></a>匯入 Java 金鑰存放區中的 SSL 憑證
Fips，很可能是您要匯入憑證 (.cert) PKCS 或提供者專屬格式。
使用下列程式碼片段匯入 SSL 憑證，並將其儲存在工作目錄中具有適當的金鑰存放區格式。 _信任\_存放區\_密碼_Java 金鑰存放區是您的密碼。

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

下列範例會匯入與 BouncyCastle 提供者 PKCS12 格式中的 Azure 」 的 SSL 憑證。 在名為的工作目錄匯入憑證_MyTrustStore\_PKCS12_使用下列程式碼片段：

`saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer");`

## <a name="appropriate-policy-files"></a>適當的原則檔案
對於某些 FIPS 提供者，需要不受限制的原則 jar。 在這種情況下，sun / Oracle 下載 Java 密碼編譯延伸模組 (JCE) 無限制強度管轄權原則檔[JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)或是[JRE 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)。 

## <a name="appropriate-configuration-parameters"></a>適當的組態參數
若要在符合 FIPS 規範的模式下執行 JDBC 驅動程式，請設定連接屬性下, 表所示。 

#### <a name="properties"></a>屬性 

|屬性|類型|預設|Description|注意|
|---|---|---|---|---|
|encrypt|boolean ["true / false"]|"false"|已啟用 FIPS 的 JVM 加密屬性應該是 **，則為 true**||
|TrustServerCertificate|boolean ["true / false"]|"false"|使用者需要驗證憑證鏈結，因此使用者應該使用 FIPS，如 **"false"** 這個屬性的值。 ||
|trustStore|String|null|您的 Java Keystore 檔案路徑您匯入您的憑證。 如果您在您的系統，則不需要傳遞任何項目上安裝憑證。 驅動程式會使用 cacerts 或 jssecacerts 檔案。||
|trustStorePassword|String|null|用於檢查 trustStore 資料完整性的密碼。||
|fips|boolean ["true / false"]|"false"|這個屬性應該是針對啟用 FIPS 的 JVM **，則為 true**|加入 6.1.4 (穩定版本 6.2.2)||
|fipsProvider|String|null|FIPS 的 JVM 設定提供者。 例如，BCFIPS 或 SunPKCS11 NSS |6.1.2 中新增 (穩定版本 6.2.2)，在 6.4.0-已被取代，請參閱詳細資料[此處](https://github.com/Microsoft/mssql-jdbc/pull/460)。|
|trustStoreType|String|JKS|FIPS 模式設定的信任存放區類型 PKCS12 或型別定義 FIPS 提供者 |6.1.2 中新增 (穩定版本 6.2.2)||
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
