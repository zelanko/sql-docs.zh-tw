---
title: "JDBC driver 的國際功能 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bbb74a1d-9278-401f-9530-7b5f45aa79de
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8b319e0fe0972b236c03694899c5d4361dbcc473
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="international-features-of-the-jdbc-driver"></a>JDBC Driver 的國際功能
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  國際化功能[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]如下：  
  
-   支援針對相同語言的完整當地語系化體驗[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
-   支援區分地區設定的 Java 語言轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料  
  
-   支援不論作業系統為何的國際語言  
  
-   支援國際網域名稱 (從 Microsoft JDBC Driver 6.0 for SQL Server 開始)  
  
## <a name="handling-of-character-data"></a>處理字元資料  
 在 Java 中的字元資料是由預設值則處理為 Unicode使用 Java**字串**物件都代表 Unicode 字元資料。 在 JDBC Driver 中，此規則唯一的例外狀況為 ASCII 資料流的 getter 與 setter 方法，其為特例的原因在於它們使用位元組資料流，並隱含的假設會使用單一已知字碼頁 (ASCII)。  
  
 此外，JDBC 驅動程式提供**sendStringParametersAsUnicode**連接字串屬性。 這個屬性可用來指定字元資料的準備參數會當做 ASCII 或多位元組字元集 (MBCS) 而非 Unicode 傳送。 如需有關**sendStringParametersAsUnicode**連接字串屬性，請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
### <a name="driver-incoming-conversions"></a>驅動程式內送轉換  
 來自伺服器的 Unicode 文字資料無需轉換。 它將直接以 Unicode 傳遞。 來自伺服器的非 Unicode 資料將在資料庫或資料行的層級中，從資料的字碼頁轉換成 Unicode。 JDBC 驅動程式使用 Java Virtual Machine (JVM) 轉換常式執行這些轉換。 這些轉換將在所有具類型的字串與字元資料流 getter 方法中執行。  
  
 如果 JVM 沒有適合的字碼頁可支援資料庫的資料，JDBC Driver 就會擲回「Java 環境不支援字碼頁 XXX」的例外狀況。 若要解決此問題，您應該安裝該 JVM 所需的完整國際字元支援。 如需範例，請參閱 Sun Microsystems 網站上的「支援的編碼」文件。  
  
### <a name="driver-outgoing-conversions"></a>驅動程式外寄轉換  
 從驅動程式送至伺服器的字元資料可以是 ASCII 或 Unicode。 例如，新 JDBC 4.0 國家字元方法，例如 setNString、 setNCharacterStream、 和 setNClob 方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別一律將參數值傳送至以 Unicode 伺服器。  
  
 另一方面，非國家字元 API 方法，例如 setString、 setCharacterStream、 和 setClob 方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別將值傳送至以 Unicode 伺服器時，才**sendStringParametersAsUnicode**屬性設定為"true"，這是預設值。  
  
## <a name="non-unicode-parameters"></a>非 Unicode 參數  
 為了達到最佳效能與**CHAR**， **VARCHAR**或**LONGVARCHAR**非 Unicode 參數的類型，設定**sendStringParametersAsUnicode**連接字串屬性設定為"false"並且使用非國家字元方法。  
  
## <a name="formatting-issues"></a>格式化問題  
 針對日期、 時間和貨幣，以執行所有格式化當地語系化資料是在 Java 語言層級使用的地區設定物件。各種格式的方法和**日期**，**行事曆**，和**數目**資料型別。 在極少的情況下，若 JDBC 驅動程式 必須以當地語系化格式傳遞區分地區設定的資料，此時適合的格式化工具便是使用預設的 JVM 地區設定。  
  
## <a name="collation-support"></a>定序支援  
 JDBC 驅動程式 3.0 支援所支援的所有定序[!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]， [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]，和新的定序或新版 Windows 定序名稱中導入[!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]。  
  
 如需有關定序的詳細資訊，請參閱[Collation and Unicode Support](http://go.microsoft.com/fwlink/?LinkId=131366)和[Windows 定序名稱 (TRANSACT-SQL)](http://go.microsoft.com/fwlink/?LinkId=131367)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="using-international-domain-names-idn"></a>使用國際網域名稱 (IDN)  
 JDBC Driver 6.0 for SQL Server 支援使用國際化網域名稱 (Idn)，並可以將 Unicode serverName 轉換成 ASCII 相容編碼 (Punycode 需要在連線時)。  如果 IDN 在網域名稱系統 (DNS) 中以 Punycode 格式 (由 RFC 3490 指定) 儲存為為 ASCII 字串，請將 serverNameAsACE 屬性設定為 true，啟用 Unicode 伺服器名稱的轉換。  否則，如果 DNS 服務設定為允許使用 Unicode 字元，則請將 serverNameAsACE 屬性設定為 false (預設值)。  對於較舊版本的 JDBC 驅動程式，您也可將 serverName 轉換為 Punycode 使用[Java 的 IDN.toASCII](http://docs.oracle.com/javase/8/docs/api/java/net/IDN.html)方法之前設定該屬性的連接。  
  
> [!NOTE]  
>  為非 Windows 平台所撰寫的大部分解析程式軟體，均以網際網路 DSN 標準為基礎，因此，最有可能為 IDN 使用 Punycode 格式，而私人網路上的 Windows DNS 伺服器，則可設定為允許在每部伺服器上使用 UTF-8 字元。  如需詳細資訊，請參閱[Unicode 字元支援](https://technet.microsoft.com/library/cc738403(v=ws.10).aspx)。  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

