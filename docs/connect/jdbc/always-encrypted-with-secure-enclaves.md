---
title: 使用具有安全記憶體保護區的 Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 01/29/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: reneye
ms.author: v-reye
ms.openlocfilehash: 441adf8e3623f06bfa98718ebc6c01c314c94828
ms.sourcegitcommit: 4b2c9d648b7a7bdf9c3052ebfeef182e2f9d66af
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/04/2020
ms.locfileid: "77004707"
---
# <a name="using-always-encrypted-with-the-secure-enclaves"></a>使用具有安全記憶體保護區的 Always Encrypted
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此頁面提供如何使用[具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md) 與 Microsoft JDBC Driver 8.2 for SQL Server (或更高版本) 來開發 Java 應用程式的相關資訊。

安全記憶體保護區是現有 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 功能的補充項目。 安全記憶體保護區目的是要解決使用 Always Encrypted 資料時的限制。 之前，使用者只能對 Always Encrypted 資料執行相等比較，且必須擷取資料並進行解密，才能執行其他作業。 安全記憶體保護區可解決這項限制，方法是允許在伺服器端的安全記憶體保護區內部進行純文字資料計算。 安全記憶體保護區是 SQL Server 處理序內受保護的記憶體區域，並可作為受信任的執行環境來處理 SQL Server 引擎內部的敏感性資料。 安全記憶體保護區對於主控電腦上其餘部分的 SQL Server 和其他處理序會顯示為黑盒子。 即使使用偵錯工具，也沒有辦法從外部檢視記憶體保護區內部的任何資料或程式碼。

## <a name="prerequisites"></a>Prerequisites
- 確定已在您的開發電腦上安裝 Microsoft JDBC Driver 8.2 for SQL Server (或更高版本)。 

> [!Note]
> 如果您使用的是舊版的 JDK 8，則可能需要下載並安裝 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔。 請務必閱讀 ZIP 檔案中的讀我檔案，以了解安裝指示及可能的匯出/匯入問題相關詳細資料。  
>
> 您可以從 [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 8 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) (下載 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔 8) 下載原則檔

## <a name="setting-up-secure-enclaves"></a>設定安全記憶體保護區
遵循此[教學課程](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md)即可開始使用安全記憶體保護區。 如需詳細的深入資訊，請參閱[具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。

## <a name="connection-string-properties"></a>連接字串屬性
**enclaveAttestationUrl：** 證明服務的端點 URL。

**enclaveAttestationProtocol：** 證明服務的通訊協定。 目前唯一支援的值為 **HGS** (主機守護者服務)。

使用者必須啟用 **columnEncryptionSetting**，並正確地設定上述**這兩個**連接字串屬性，才能從 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 啟用具有安全記憶體保護區的 Always Encrypted。

## <a name="working-with-secure-enclaves"></a>使用安全記憶體保護區
當記憶體保護區連線屬性設定正確時，此功能將會以透明方式運作。 驅動程式會自動判斷查詢是否需要使用安全記憶體保護區。 下列為觸發記憶體保護區計算的查詢範例。 您可以在[開始使用 Always Encrypted 記憶體保護區](../../relational-databases/security/tutorial-getting-started-with-always-encrypted-enclaves.md)中找到資料庫和資料表設定。

豐富的查詢將會觸發記憶體保護區計算：
```java
private static final String URL = "jdbc:sqlserver://<server>:<port>;user=<username>;password=<password>;databaseName=ContosoHR;columnEncryptionSetting=enabled;enclaveAttestationUrl=<attestation-url>;enclaveAttestationProtocol=<attestation-protocol>;";
try (Connection c = DriverManager.getConnection(URL)) {
    try (PreparedStatement p = c.prepareStatement("SELECT * FROM Employees WHERE SSN LIKE ?")) {
        p.setString(1, "%6818");
        try (ResultSet rs = p.executeQuery()) {
            while (rs.next()) {
                // Do work with data
            }
        }
    }
    
    try (PreparedStatement p = c.prepareStatement("SELECT * FROM Employees WHERE SALARY > ?")) {
        ((SQLServerPreparedStatement) p).setMoney(1, new BigDecimal(0));
        try (ResultSet rs = p.executeQuery()) {
            while (rs.next()) {
                // Do work with data
            }
        }
    }
}
```

切換資料行的加密也會觸發記憶體保護區計算：
```java
private static final String URL = "jdbc:sqlserver://<server>:<port>;user=<username>;password=<password>;databaseName=ContosoHR;columnEncryptionSetting=enabled;enclaveAttestationUrl=<attestation-url>;enclaveAttestationProtocol=<attestation-protocol>;";
try (Connection c = DriverManager.getConnection(URL);Statement s = c.createStatement()) {
    s.executeUpdate("ALTER TABLE Employees ALTER COLUMN SSN CHAR(11) NULL WITH (ONLINE = ON)");
}
```

## <a name="java-8-users"></a>Java 8 使用者
這項功能需要 RSASSA-PSA 簽章演算法。 此演算法已於 JDK 11 中新增，但並未回溯移植至 JDK 8。 想要使用這項功能搭配 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] JDK 8 版本的使用者，必須載入自己的提供者，以支援 RSASSA-PSA 簽章演算法，或包含 BouncyCastleProvider 選擇性相依性。 如果 JDK 8 回溯移植此簽章演算法，或 JDK 8 的支援生命週期結束，即會在日後移除該項相依性。

## <a name="see-also"></a>另請參閱
[搭配 JDBC 驅動程式使用 Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  