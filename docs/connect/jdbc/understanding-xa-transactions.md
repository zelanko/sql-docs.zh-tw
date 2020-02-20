---
title: 了解 XA 交易 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 574e326f-0520-4003-bdf1-62d92c3db457
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e249bb515ca0a8b579e923e7d289fccd80ce6ef
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "74947130"
---
# <a name="understanding-xa-transactions"></a>了解 XA 交易

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供 Java Platform Enterprise Edition/JDBC 2.0 選擇性分散式交易的支援。 從 [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) 類別取得的 JDBC 連線可參與標準分散式交易處理環境，例如 Java Platform Enterprise Edition (Java EE) 應用程式伺服器。  

在此文章中，XA 代表延伸架構。

> [!WARNING]  
> Microsoft JDBC Driver 4.2 (和更新版本) for SQL 包含新的現有功能逾時選項，用於已取消準備交易的自動回復。 如需詳細資訊，請參閱此主題稍後的[針對已取消準備之交易的自動回復設定伺服器端逾時設定](../../connect/jdbc/understanding-xa-transactions.md#BKMK_ServerSide)。  

## <a name="remarks"></a>備註

分散式交易實作的類別如下：  
  
| 類別                                              | 實作                      | 描述                                       |
| -------------------------------------------------- | ------------------------------- | ------------------------------------------------- |
| com.microsoft.sqlserver.jdbc.SQLServerXADataSource | javax.sql.XADataSource          | 分散式連接的 Class Factory。    |
| com.microsoft.sqlserver.jdbc.SQLServerXAResource   | javax.transaction.xa.XAResource | 交易管理員的資源配接器。 |
  
> [!NOTE]  
> XA 分散式交易連接會預設為「讀取認可」隔離等級。  
  
## <a name="guidelines-and-limitations-when-using-xa-transactions"></a>使用 XA 交易時的指導方針和限制  

下列額外指導方針適用於緊密繫結的交易：  

- 當您將 XA 交易與 Microsoft 分散式交易協調器 (MS DTC) 一起使用時，可能會注意到目前版本的 MS DTC 不支援緊密繫結的 XA 分支行為。 例如，MS DTC 在 XA 分支交易識別碼 (XID) 與 MS DTC 交易識別碼之間擁有一對一的對應，而且由鬆散繫結之 XA 分支所執行的工作會彼此隔離。  
  
- MSDTC 也支援緊密耦合的 XA 分支，其中具有相同全域交易識別碼 (GTRID) 的多個 XA 分支會對應到單一 MS DTC 交易識別碼。 此支援讓多個緊密結合的 XA 分支可以在資源管理員 (例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 中查看彼此的變更。
  
- [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) 旗標允許應用程式使用緊密結合的 XA 交易，但這些交易的 XA 分支交易識別碼 (BQUAL) 各不相同，只有全域交易識別碼 (GTRID) 及格式識別碼 (FormatID) 相同。 若要使用該功能，您必須在 XAResource.start 方法的 flags 參數上，設定 [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)：
  
    ```java
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);  
    ```  
  
## <a name="configuration-instructions"></a>設定指示

如果要將 XA 資料來源與 Microsoft 分散式交易協調器 (MS DTC) 搭配使用，來處理分散式交易，則需要下列步驟。  

> [!NOTE]  
> JDBC 分散式交易元件會包含在 JDBC 驅動程式安裝的 xa 目錄中。 這些元件包括 xa_install.sql 及 sqljdbc_xa.dll 檔案。  

> [!NOTE]  
> 從 SQL Server 2019 公開預覽 CTP 2.0 開始，JDBC XA 分散式交易元件會包含在 SQL Server 引擎中，並且可以使用系統預存程序來啟用或停用。
> 若要使用 JDBC 驅動程式啟用必要元件以執行 XA 分散式交易，請執行下列預存程序。
>
> EXEC sp_sqljdbc_xa_install
>
> 若要停用先前安裝的元件，請執行下列預存程序。
>
> EXEC sp_sqljdbc_xa_uninstall

### <a name="running-the-ms-dtc-service"></a>執行 MS DTC 服務

應該在服務管理員中將 MS DTC 服務標示為 [自動]  ，以確定啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務時，便執行該服務。 若要啟用 MS DTC 以用於 XA 交易，您必須遵循下列步驟：  
  
在 Windows Vista 及更新的版本上：  
  
1. 按一下 [開始]  按鈕、在 [開始搜尋]  方塊中鍵入 **dcomcnfg**，然後按下 ENTER 開啟 [元件服務]  。 您也可以在 [開始搜尋]  方塊中鍵入 %windir%\system32\comexp.msc，開啟 [元件服務]  。  
  
2. 依序展開 [元件服務]、[電腦]、[我的電腦] 和 [分散式交易協調器]。  
  
3. 以滑鼠右鍵按一下 [本機 DTC]  ，然後選取 [內容]  。  
  
4. 按一下 [本機 DTC 內容]  對話方塊中的 [安全性]  索引標籤。  
  
5. 選取 [啟用 XA 交易]  核取方塊，然後按一下 [確定]  。 MS DTC 服務會隨即重新啟動。
  
6. 再按一下 [確定]  關閉 [內容]  對話方塊，然後關閉 [元件服務]  。  
  
7. 停止然後重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，以確保其與 MS DTC 變更保持同步。  

### <a name="configuring-the-jdbc-distributed-transaction-components"></a>設定 JDBC 分散式交易元件  

您可以遵循下列步驟，來設定 JDBC 驅動程式分散式交易元件：  
  
1. 將新的 sqljdbc_xa.dll 從 JDBC 驅動程式安裝目錄複製到將參與分散式交易之每一部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦的 Binn 目錄。  
  
    > [!NOTE]  
    > 如果您搭配 32 位元的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 XA 交易，即使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝在 x64 處理器上，也請使用 x86 資料夾中的 sqljdbc_xa.dll 檔案。 如果您在 x64 處理器上，搭配 64 位元的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 XA 交易，請使用 x64 資料夾中的 sqljdbc_xa.dll 檔。  
  
2. 在每一個將參與分散式交易的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上執行資料庫指令碼 xa_install.sql。 這個指令碼就會安裝 sqljdbc_xa.dll 所呼叫的擴充預存程序。 這些擴充預存程序會實作 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的分散式交易和 XA 支援。 您將需要以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的系統管理員身分執行此指令碼。  
  
3. 若要授與權限給特定使用者以使用 JDBC Driver 參與分散式交易，請將該使用者新增至 SqlJDBCXAUser 角色。  
  
您一次只能針對每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體設定單一 sqljdbc_xa.dll 組件版本。 應用程式可能必須使用不同的 JDBC 驅動程式版本，透過 XA 連線連線到相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 在該情況下，您就必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上安裝隨附於最新 JDBC 驅動程式的 sqljdbc_xa.dll。  
  
有三種方式可以確認目前安裝在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的 sqljdbc_xa.dll 版本：
  
1. 開啟將參與分散式交易之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦的 LOG 目錄。 選取並開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "ERRORLOG" 檔案。 在 "ERRORLOG" 檔案中搜尋 "Using 'SQLJDBC_XA.dll' version ..." 片語。  
  
2. 開啟將參與分散式交易之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦的 Binn 目錄。 選取 sqljdbc_xa.dll 組件。

    - 在 Windows Vista 或更新的版本上：以滑鼠右鍵按一下 sqljdbc_xa.dll，然後選取 [內容]。 然後，按一下 [詳細資料]  索引標籤。[檔案版本]  欄位就會顯示目前安裝在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的 sqljdbc_xa.dll 版本。  
  
3. 依照下一節的程式碼範例所示，設定記錄功能。 在輸出記錄檔案中搜尋 "Server XA DLL version:..." 片語。  

### <a name="BKMK_ServerSide"></a> 針對已取消準備之交易的自動回復設定伺服器端逾時設定  

> [!WARNING]  
> 此伺服器端選項是 Microsoft JDBC Driver 4.2 (或更高版本) for SQL Server 的新功能。 若要取得更新過的表現方式，請務必更新伺服器上的 sqljdbc_xa.dll。 如需設定用戶端逾時值的詳細資訊，請參閱 [XAResource.setTransactionTimeout()](https://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAResource.html)。  

有兩個登錄設定 (DWORD 值) 用來控制分散式交易的逾時行為：  
  
- **XADefaultTimeout** (以秒為單位)：若使用者未指定任何逾時，此時所要使用的預設逾時值。 預設值是 0。  
  
- **XAMaxTimeout** (以秒為單位)：使用者可以設定的逾時最大值。 預設值是 0。  
  
這些是 SQL Server 執行個體的特定設定，而且應該建立在下列登錄機碼底下：  

```bash
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout  
```

> [!NOTE]  
> 在 64 位元機器中執行的 32 位元 SQL Server，應在下列機碼底下建立登錄設定：`HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout`
  
如果逾時到期，當此設定已啟動且交易已由 SQL Server 回復時，會設定每一筆交易的逾時值。 根據這些登錄設定，並根據使用者已透過 XAResource.setTransactionTimeout() 指定的設定，來決定此逾時。 這些逾時值解譯方式的幾個範例，如下所示：  
  
- `XADefaultTimeout = 0`, `XAMaxTimeout = 0`
  
     表示不使用預設的逾時，在用戶端上將不強制執行最大逾時。 在此情況下，只有當用戶端使用 XAResource.setTransactionTimeout 設定逾時，此交易才會有逾時。  
  
- `XADefaultTimeout = 60`, `XAMaxTimeout = 0`
  
     表示如果用戶端未指定任何逾時，則所有交易都會都有 60 秒逾時。 如果用戶端指定了逾時，則會使用該逾時值。 不會強制執行逾時最大值。  
  
- `XADefaultTimeout = 30`, `XAMaxTimeout = 60`
  
     表示如果用戶端未指定任何逾時，則所有交易都會都有 30 秒逾時。 用戶端如有指定逾時，除非該值小於 60 秒 (最大值)，否則將會使用用戶端的逾時值。  
  
- `XADefaultTimeout = 0`, `XAMaxTimeout = 30`
  
     表示如果用戶端未指定任何逾時，則所有交易都會都有 30 秒逾時 (最大值)。 用戶端如有指定逾時，除非該值小於 30 秒 (最大值)，否則將會使用用戶端的逾時值。  
  
### <a name="upgrading-sqljdbc_xadll"></a>升級 sqljdbc_xa.dll

當您安裝新版 JDBC 驅動程式時，也應該使用新版的 sqljdbc_xa.dll 來升級伺服器上的 sqljdbc_xa.dll。  
  
> [!IMPORTANT]  
> 您應利用維護時段，或沒有任何 MS DTC 交易正在進行時，升級 sqljdbc_xa.dll。
  
1. 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令 **DBCC sqljdbc_xa (FREE)** 來卸載 sqljdbc_xa.dll。  
  
2. 將新的 sqljdbc_xa.dll 從 JDBC 驅動程式安裝目錄複製到將參與分散式交易之每一部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦的 Binn 目錄。  
  
    當系統呼叫 sqljdbc_xa.dll 中的擴充程序時，就會載入新的 DLL。 您不需要重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以載入新的定義。  
  
### <a name="configuring-the-user-defined-roles"></a>設定使用者定義角色

若要授與權限給特定使用者以使用 JDBC Driver 參與分散式交易，請將該使用者新增至 SqlJDBCXAUser 角色。 例如，使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，將名為 'shelby' (SQL 標準登入使用者名稱為 'shelby') 的使用者新增至 SqlJDBCXAUser 角色：  

```sql
USE master  
GO  
EXEC sp_grantdbaccess 'shelby', 'shelby'  
GO  
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelby'  
```

每一個資料庫都會定義 SQL 使用者自訂角色。 若要基於安全目的來建立您自己的角色，您將必須在每一個資料庫中定義角色，然後在每一個資料庫中新增使用者。 SqlJDBCXAUser 角色一定是定義在 master 資料庫中，因為它是用來授與存取 SQL JDBC 擴充預存程序 (位於 master 資料庫) 的權限。 您必須先授與個別使用者存取 master 的權限，然後在您登入 master 資料庫時，再授與他們存取 SqlJDBCXAUser 角色的權限。  

## <a name="example"></a>範例  

```java
import java.net.Inet4Address;
import java.sql.*;
import java.util.Random;
import javax.sql.XAConnection;
import javax.transaction.xa.*;
import com.microsoft.sqlserver.jdbc.*;


public class testXA {

    public static void main(String[] args) throws Exception {

        // Create variables for the connection string.
        String prefix = "jdbc:sqlserver://";
        String serverName = "localhost";
        int portNumber = 1433;
        String databaseName = "AdventureWorks";
        String user = "UserName";
        String password = "*****";

        String connectionUrl = prefix + serverName + ":" + portNumber + ";databaseName=" + databaseName + ";user="
                + user + ";password=" + password;

        Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement()) {
            stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");

        }
        // Create the XA data source and XA ready connection.
        SQLServerXADataSource ds = new SQLServerXADataSource();
        ds.setUser(user);
        ds.setPassword(password);
        ds.setServerName(serverName);
        ds.setPortNumber(portNumber);
        ds.setDatabaseName(databaseName);

        XAConnection xaCon = ds.getXAConnection();
        try (Connection con = xaCon.getConnection()) {

            // Get a unique Xid object for testing.
            XAResource xaRes = null;
            Xid xid = null;
            xid = XidImpl.getUniqueXid(1);

            // Get the XAResource object and set the timeout value.
            xaRes = xaCon.getXAResource();
            xaRes.setTransactionTimeout(0);

            // Perform the XA transaction.
            System.out.println("Write -> xid = " + xid.toString());
            xaRes.start(xid, XAResource.TMNOFLAGS);
            PreparedStatement pstmt = con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");
            pstmt.setInt(1, 1);
            pstmt.setString(2, xid.toString());
            pstmt.executeUpdate();

            // Commit the transaction.
            xaRes.end(xid, XAResource.TMSUCCESS);
            xaRes.commit(xid, true);
        }
        xaCon.close();

        // Open a new connection and read back the record to verify that it worked.
        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT * FROM XAMin")) {
            rs.next();
            System.out.println("Read -> xid = " + rs.getString(2));
            stmt.executeUpdate("DROP TABLE XAMin");
        }
    }
}


class XidImpl implements Xid {

    public int formatId;
    public byte[] gtrid;
    public byte[] bqual;

    public byte[] getGlobalTransactionId() {
        return gtrid;
    }

    public byte[] getBranchQualifier() {
        return bqual;
    }

    public int getFormatId() {
        return formatId;
    }

    XidImpl(int formatId, byte[] gtrid, byte[] bqual) {
        this.formatId = formatId;
        this.gtrid = gtrid;
        this.bqual = bqual;
    }

    public String toString() {
        int hexVal;
        StringBuffer sb = new StringBuffer(512);
        sb.append("formatId=" + formatId);
        sb.append(" gtrid(" + gtrid.length + ")={0x");
        for (int i = 0; i < gtrid.length; i++) {
            hexVal = gtrid[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(gtrid[i] & 0xFF));
            else
                sb.append(Integer.toHexString(gtrid[i] & 0xFF));
        }
        sb.append("} bqual(" + bqual.length + ")={0x");
        for (int i = 0; i < bqual.length; i++) {
            hexVal = bqual[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(bqual[i] & 0xFF));
            else
                sb.append(Integer.toHexString(bqual[i] & 0xFF));
        }
        sb.append("}");
        return sb.toString();
    }

    // Returns a globally unique transaction id.
    static byte[] localIP = null;
    static int txnUniqueID = 0;

    static Xid getUniqueXid(int tid) {

        Random rnd = new Random(System.currentTimeMillis());
        txnUniqueID++;
        int txnUID = txnUniqueID;
        int tidID = tid;
        int randID = rnd.nextInt();
        byte[] gtrid = new byte[64];
        byte[] bqual = new byte[64];
        if (null == localIP) {
            try {
                localIP = Inet4Address.getLocalHost().getAddress();
            } catch (Exception ex) {
                localIP = new byte[] {0x01, 0x02, 0x03, 0x04};
            }
        }
        System.arraycopy(localIP, 0, gtrid, 0, 4);
        System.arraycopy(localIP, 0, bqual, 0, 4);

        // Bytes 4 -> 7 - unique transaction id.
        // Bytes 8 ->11 - thread id.
        // Bytes 12->15 - random number generated by using seed from current time in milliseconds.
        for (int i = 0; i <= 3; i++) {
            gtrid[i + 4] = (byte) (txnUID % 0x100);
            bqual[i + 4] = (byte) (txnUID % 0x100);
            txnUID >>= 8;
            gtrid[i + 8] = (byte) (tidID % 0x100);
            bqual[i + 8] = (byte) (tidID % 0x100);
            tidID >>= 8;
            gtrid[i + 12] = (byte) (randID % 0x100);
            bqual[i + 12] = (byte) (randID % 0x100);
            randID >>= 8;
        }
        return new XidImpl(0x1234, gtrid, bqual);
    }
}

```

## <a name="see-also"></a>另請參閱  

[以 JDBC 驅動程式執行交易](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
