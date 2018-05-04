---
title: 在 FIPS 模式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 1
author: v-nisidh
ms.author: v-nisidh
manager: andrela
ms.openlocfilehash: fb8e6d19ef4359ebc16ed1089561c23724d7a34b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="fips-mode"></a>在 FIPS 模式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver for SQL Server 支援*FIPS 140 標準模式*。 Oracle / Sun JVM，請參閱[SunJSSE 的 FIPS 140 標準模式下](https://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/FIPS.html)啟用 JVM 所設定的 FIPS Oracle 提供的區段。 

**必要條件**:
* FIPS 設定 JVM
* 適當的 SSL 憑證。
* 適當的原則檔案。 
* 適當的組態參數。 


## <a name="fips-configured-jvm"></a>FIPS 設定 JVM

若要查看 FIPS 設定的已核准的模組，請參閱[驗證 FIPS 140-1 和 FIPS 140-2 的密碼編譯模組](http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/1401val2016.htm)。 

廠商可能會有一些額外步驟以 fips 設定 JVM。

### <a name="ensure-your-jvm-is-in-fips-mode"></a>請確定您的 JVM 處於啟用 FIPS 模式
若要確保您的 JVM FIPS 已啟用，請執行下列程式碼片段： 

````
public boolean isFIPS() throws Exception {
    Provider jsse = Security.getProvider("SunJSSE");
    return jsse != null && jsse.getInfo().contains("FIPS");
}
````

## <a name="appropriate-ssl-certificate"></a>適當的 SSL 憑證
為了在 FIPS 模式中，連接 SQL Server，都需要有效的 SSL 憑證。 安裝或匯入 Java 金鑰存放區中用戶端機器 (JVM) 上啟用 FIPS 的位置。 如果您沒有匯入 / 安裝適當的憑證，您可能無法連接到 SQL Server 無法建立安全連接。

### <a name="importing-ssl-certificate-in-java-keystore"></a>匯入 Java 金鑰存放區中的 SSL 憑證
為 FIPS，很可能是您需要 (.cert) 將憑證匯入至任一 PKCS 或提供者特定格式。 使用下列程式碼片段匯入 SSL 憑證，並將其儲存在工作目錄中並且在適當的金鑰存放區格式。 _TRUST_STORE_PASSWORD_ Java 金鑰存放區中為您的密碼。 

````
    public void saveGenericKeyStore(String provider, String trustStoreType, String certName, String certPath) throws KeyStoreException, CertificateException, NoSuchAlgorithmException, NoSuchProviderException, IOException {
        KeyStore ks = KeyStore.getInstance(trustStoreType, provider);
        FileOutputStream os = new FileOutputStream("./MyTrustStore_" + trustStoreType);
        ks.load(null, null);
        ks.setCertificateEntry(certName, getCertificate(certPath));
        ks.store(os, TRUST_STORE_PASSWORD.toCharArray());
        os.flush();
        os.close();
    }

    private Certificate getCertificate(String pathName) throws FileNotFoundException, CertificateException {
        FileInputStream fis = new FileInputStream(pathName);
        CertificateFactory cf = CertificateFactory.getInstance("X.509");
        return cf.generateCertificate(fis);
    }

````


下列範例會匯入 Azure SSL 憑證 PKCS12 格式與 BouncyCastle 提供者。 在名為的工作目錄匯入憑證_MyTrustStore_PKCS12_使用下列程式碼片段：

` saveGenericKeyStore(BCFIPS, PKCS12, "SQLAzure SSL Certificate Name", "SQLAzure.cer"); `

## <a name="appropriate-policy-files"></a>適當的原則檔案
對於某些 FIPS 提供者，需要不受限制的原則 （每瓶）。 在這種情況下，如 Sun / Oracle 下載 Java 密碼編譯延伸模組 (JCE) 無限制強度管轄權原則檔[JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)或[JRE 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)。 

## <a name="appropriate-configuration-parameters"></a>適當的組態參數
若要在 FIPS 相容模式下執行 JDBC 驅動程式，設定連接屬性，如下表所示。 

**屬性**: 

|屬性|型別|預設值|Description|注意|
|---|---|---|---|---|
|encrypt|布林值 ["，則為 true / false"]|"false"|JVM 已啟用則為 FIPS 加密屬性應該是**，則為 true**||
|TrustServerCertificate|布林值 ["，則為 true / false"]|"false"|使用者必須要驗證憑證鏈結，因此，使用者應該使用 FIPS， **"false"** 這個屬性的值。 ||
|trustStore|字串|null|您匯入您的憑證的 Java Keystore 檔案路徑。 如果您的系統，則不需要傳遞任何項目上安裝憑證。 驅動程式會使用 cacerts 或 jssecacerts 檔案。||
|trustStorePassword|字串|null|用於檢查 trustStore 資料完整性的密碼。||
|fips|布林值 ["，則為 true / false"]|"false"|這個屬性應該是 fips 已啟用則為 JVM **，則為 true**|加入 6.1.4 (穩定版本 6.2.2)||
|fipsProvider|字串|null|JVM 中所設定的 FIPS 提供者。 例如，BCFIPS 或 SunPKCS11 NSS |6.1.2 中加入 (穩定版本 6.2.2)，6.4.0-中已被取代，請參閱詳細資料[這裡](https://github.com/Microsoft/mssql-jdbc/pull/460)。|
|trustStoreType|字串|JKS|FIPS 模式設定的信任存放區類型 PKCS12 或型別定義 FIPS 提供者 |6.1.2 中加入 (穩定版本 6.2.2)||



  
