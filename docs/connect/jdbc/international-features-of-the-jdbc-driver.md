---
description: JDBC 驅動程式的國際功能
title: JDBC 驅動程式的國際功能 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bbb74a1d-9278-401f-9530-7b5f45aa79de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 960f689f39007b4fbe4d7aa01d935ef1aaf640cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438400"
---
# <a name="international-features-of-the-jdbc-driver"></a>JDBC 驅動程式的國際功能
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的國際化功能包含下列各項：  
  
-   支援與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相同語言的完整當地語系化體驗  
  
-   支援區分地區設定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的 Java 語言轉換  
  
-   支援不論作業系統為何的國際語言  
  
-   支援國際網域名稱 (從 Microsoft JDBC Driver 6.0 for SQL Server 開始)  
  
## <a name="handling-of-character-data"></a>處理字元資料  
 Java 的字元資料預設是以 Unicode 來處理；Java **String** 物件則代表 Unicode 字元資料。 在 JDBC Driver 中，此規則唯一的例外狀況為 ASCII 資料流的 getter 與 setter 方法，其為特例的原因在於它們使用位元組資料流，並隱含的假設會使用單一已知字碼頁 (ASCII)。  
  
 此外，JDBC 驅動程式會提供 **sendStringParametersAsUnicode** 連接字串屬性。 這個屬性可用來指定字元資料的準備參數會當做 ASCII 或多位元組字元集 (MBCS) 而非 Unicode 傳送。 如需有關 **sendStringParametersAsUnicode** 連接字串屬性的詳細資訊，請參閱[設定連線屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
### <a name="driver-incoming-conversions"></a>驅動程式內送轉換  
 來自伺服器的 Unicode 文字資料無需轉換。 它將直接以 Unicode 傳遞。 來自伺服器的非 Unicode 資料將在資料庫或資料行的層級中，從資料的字碼頁轉換成 Unicode。 JDBC 驅動程式使用 Java Virtual Machine (JVM) 轉換常式執行這些轉換。 這些轉換將在所有具類型的字串與字元資料流 getter 方法中執行。  
  
 如果 JVM 沒有適合的字碼頁可支援資料庫的資料，JDBC Driver 就會擲回「Java 環境不支援字碼頁 XXX」的例外狀況。 若要解決此問題，您應該安裝該 JVM 所需的完整國際字元支援。 如需範例，請參閱 Sun Microsystems 網站上的「支援的編碼」文件。  
  
### <a name="driver-outgoing-conversions"></a>驅動程式外寄轉換  
 從驅動程式送至伺服器的字元資料可以是 ASCII 或 Unicode。 例如，新的 JDBC 4.0 國際字元方法 (例如 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別的 setNString、setNCharacterStream 及 setNClob methods方法) 一律會以 Unicode 將其參數值傳送到伺服器。  
  
 另一方面，非國際字元 API 方法 (例如 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 與 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別的 setString、setCharacterStream 與 setClob 方法) 則只有當 **sendStringParametersAsUnicode** 屬性設定為 "true" 時 (預設值)，才會將其值以 Unicode 傳送至伺服器。  
  
## <a name="non-unicode-parameters"></a>非 Unicode 參數  
 若要取得非 Unicode 參數的 **CHAR**、**VARCHAR** 或 **LONGVARCHAR** 類型的最佳效能，請將 **sendStringParametersAsUnicode** 連接字串屬性設定為 "false" 並且使用非國家字元方法。  
  
## <a name="formatting-issues"></a>格式化問題  
 針對日期、時間及貨幣，都會使用 Locale 物件，在 Java 語言層級中以當地語系化資料執行所有格式化；以及各種 **Date**、**Calendar** 與 **Number** 資料類型的格式化方法。 在極少的情況下，若 JDBC 驅動程式 必須以當地語系化格式傳遞區分地區設定的資料，此時適合的格式化工具便是使用預設的 JVM 地區設定。  
  
## <a name="collation-support"></a>定序支援  
 JDBC Driver 3.0 支援 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 和 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 所支援的所有定序，以及 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] 中引進的新定序或新版 Windows 定序名稱。  
  
 如需定序的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的[定序與 Unicode 支援](https://go.microsoft.com/fwlink/?LinkId=131366) 和 [Windows 定序名稱 (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=131367)。  
  
## <a name="using-international-domain-names-idn"></a>使用國際網域名稱 (IDN)  
 SQL Server 的 JDBC Driver 6.0 支援使用國際化網域名稱 (IDN)，且於連線期間會於必要時將 Unicode serverName 轉換成 ASCII 相容編碼 (Punycode)。  如果 IDN 在網域名稱系統 (DNS) 中以 Punycode 格式 (由 RFC 3490 指定) 儲存為為 ASCII 字串，請將 serverNameAsACE 屬性設定為 true，啟用 Unicode 伺服器名稱的轉換。  否則，如果 DNS 服務設定為允許使用 Unicode 字元，則請將 serverNameAsACE 屬性設定為 false (預設值)。  針對舊版 JDBC 驅動程式，也可將 serverName 轉換為 Punycode，方法是在為連線設定該屬性之前，使用 [Java 的 IDN.toASCII](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html) 方法。  
  
> [!NOTE]  
>  為非 Windows 平台所撰寫的大部分解析程式軟體，均以網際網路 DSN 標準為基礎，因此，最有可能為 IDN 使用 Punycode 格式，而私人網路上的 Windows DNS 伺服器，則可設定為允許在每部伺服器上使用 UTF-8 字元。  如需詳細資料，請參閱 [Unicode 字元支援](https://technet.microsoft.com/library/cc738403(v=ws.10).aspx)。  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
