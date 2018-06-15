---
title: 了解 XA 交易 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 574e326f-0520-4003-bdf1-62d92c3db457
caps.latest.revision: 80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a78fdb7edae90289d64d4c7fdf74ac3a12d4b115
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853043"
---
# <a name="understanding-xa-transactions"></a>了解 XA 交易
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供 Java Platform，Enterprise Edition/JDBC 2.0 選擇性分散式交易支援。 從取得的 JDBC 連接[SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md)類別可參與標準分散式交易處理環境，例如 Java Platform Enterprise Edition (Java EE) 應用程式伺服器。  
  
> [!WARNING]  
>  Microsoft JDBC Driver 4.2 （和更新版本） for SQL 包含新逾時的現有自動回復功能的選項已取消準備交易。 請參閱[設定伺服器端逾時設定的自動回復已取消準備交易的](../../connect/jdbc/understanding-xa-transactions.md#BKMK_ServerSide)本主題稍後如需詳細資訊。  
  
## <a name="remarks"></a>備註  
 分散式交易實作的類別如下：  
  
|類別|實作|Description|  
|-----------|----------------|-----------------|  
|com.microsoft.sqlserver.jdbc.SQLServerXADataSource|javax.sql.XADataSource|分散式連接的 Class Factory。|  
|com.microsoft.sqlserver.jdbc.SQLServerXAResource|javax.transaction.xa.XAResource|交易管理員的資源配接器。|  
  
> [!NOTE]  
>  XA 分散式交易連接會預設為「讀取認可」隔離等級。  
  
## <a name="guidelines-and-limitations-when-using-xa-transactions"></a>使用 XA 交易時的指導方針和限制  
 下列額外指導方針適用於緊密繫結的交易：  
  
-   當您將 XA 交易與 Microsoft 分散式交易協調器 (MS DTC) 一起使用時，可能會注意到目前版本的 MS DTC 不支援緊密繫結的 XA 分支行為。 例如，MS DTC 在 XA 分支交易識別碼 (XID) 與 MS DTC 交易識別碼之間擁有一對一的對應，而且由鬆散繫結之 XA 分支所執行的工作會彼此隔離。  
  
     在提供的 hotfix [MSDTC 和緊密繫結的交易](http://support.microsoft.com/kb/938653)可以支援緊密結合的 XA 分支，其中多個 XA 分支具有相同全域交易識別碼 (GTRID) 會對應到單一 MS DTC 交易識別碼。 這個支援可讓多個緊密結合的 XA 分支查看彼此的中變更資源管理員 中，例如[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   A [SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)旗標可讓應用程式使用緊密結合的 XA 交易，這樣不同的 XA 分支交易識別碼 (BQUAL)，但具有相同全域交易識別碼 (GTRID) 和格式識別碼 (FormatID)。 若要使用該功能，您必須設定[SSTRANSTIGHTLYCPLD](../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) XAResource.start 方法的旗標參數上：  
  
    ```  
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);  
    ```  
  
## <a name="configuration-instructions"></a>組態指示  
 如果要將 XA 資料來源與 Microsoft 分散式交易協調器 (MS DTC) 搭配使用，來處理分散式交易，則需要下列步驟。  
  
> [!NOTE]  
>  JDBC 分散式交易元件會包含在 JDBC 驅動程式安裝的 xa 目錄中。 這些元件包括 xa_install.sql 及 sqljdbc_xa.dll 檔案。  
  
### <a name="running-the-ms-dtc-service"></a>執行 MS DTC 服務  
 MS DTC 服務應標示為**自動**Service Manager 中請確定它是否正在執行時[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]服務已啟動。 若要啟用 MS DTC 以用於 XA 交易，您必須遵循下列步驟：  
  
 在 Windows Vista 及更新的版本上：  
  
1.  按一下**啟動**按鈕，輸入**dcomcnfg**中開始**搜尋**方塊，然後再按下 ENTER 開啟**元件服務**。 您也可以輸入 %windir%\system32\comexp.msc 中的**開始搜尋**開啟**元件服務**。  
  
2.  依序展開 [元件服務]、[電腦]、[我的電腦] 和 [分散式交易協調器]。  
  
3.  以滑鼠右鍵按一下**本機 DTC** ，然後選取 **屬性**。  
  
4.  按一下**安全性**索引標籤上**本機 DTC 內容** 對話方塊。  
  
5.  選取**啟用 XA 交易**核取方塊，然後**確定**。 這將導致 MS DTC 服務重新啟動。  
  
6.  按一下**確定**] 以關閉 [**屬性**對話方塊，然後關閉**元件服務**。  
  
7.  停止然後再重新啟動[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]以確定其與 MS DTC 變更同步設定。  
  
### <a name="configuring-the-jdbc-distributed-transaction-components"></a>設定 JDBC 分散式交易元件  
 您可以遵循下列步驟，來設定 JDBC 驅動程式分散式交易元件：  
  
1.  將新的 sqljdbc_xa.dll 從 JDBC 驅動程式安裝目錄複製到 Binn 目錄的每個[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]電腦中會參與分散式交易。  
  
    > [!NOTE]  
    >  如果您使用 XA 交易與 32 位元[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，使用 x86 的 sqljdbc_xa.dll 檔資料夾，即使[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]安裝在 x64 處理器。 如果您使用 XA 交易與 64 位元[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]x64 上的處理器，使用在 x64 的 sqljdbc_xa.dll 檔資料夾。  
  
2.  執行資料庫指令碼 xa_install.sql 上每個[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體中，將參與分散式交易。 這個指令碼就會安裝 sqljdbc_xa.dll 所呼叫的擴充預存程序。 這些擴充預存程序會實作分散式的交易和 XA 支援[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]。 您必須以系統管理員的身分執行此指令碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體。  
  
3.  若要授與權限給特定使用者以使用 JDBC Driver 參與分散式交易，請將該使用者新增至 SqlJDBCXAUser 角色。  
  
 您可以設定每個上的 sqljdbc_xa.dll 組件只有一個版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]一次的執行個體。 應用程式可能需要使用不同版本的 JDBC 驅動程式連接到相同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]透過 XA 連接的執行個體。 在此情況下，必須安裝隨附的最新的 JDBC 驅動程式的 sqljdbc_xa.dll 上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體。  
  
 有三種方式可確認目前已安裝的 sqljdbc_xa.dll 版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體：  
  
1.  開啟記錄檔目錄的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]電腦中會參與分散式交易。 選取並開啟[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"ERRORLOG"檔案。 在 "ERRORLOG" 檔案中搜尋 "Using 'SQLJDBC_XA.dll' version ..." 片語。  
  
2.  開啟的 Binn 目錄[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]電腦中會參與分散式交易。選取 sqljdbc_xa.dll 組件。  
  
    -   在 Windows Vista 或更新版本上：以滑鼠右鍵按一下 sqljdbc_xa.dll，然後選取 [內容]。 然後按一下 [**詳細資料**] 索引標籤。**檔案版本**欄位會顯示目前已安裝的 sqljdbc_xa.dll 版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體。  
  
3.  依照下一節的程式碼範例所示，設定記錄功能。 在輸出記錄檔案中搜尋 "Server XA DLL version:..." 片語。  
  
###  <a name="BKMK_ServerSide"></a> 設定自動回復已取消準備交易的伺服器端逾時設定  
  
> [!WARNING]  
>  此伺服器端選項是新功能包含 Microsoft JDBC Driver 4.2 （和更新版本） for SQL Server。 若要取得更新過的表現方式，請務必更新伺服器上的 sqljdbc_xa.dll。 如需有關如何設定用戶端端逾時值的詳細資訊，請參閱[xaresource.settransactiontimeout （)](http://docs.oracle.com/javase/8/docs/api/javax/transaction/xa/XAResource.html)。  
  
 有兩個登錄設定 (DWORD 值) 用來控制分散式交易的逾時行為：  
  
-   **XADefaultTimeout** （以秒為單位）： 使用者未指定任何逾時所要使用的預設逾時值。 預設值是 0。  
  
-   **XAMaxTimeout** （以秒為單位）： 使用者可以設定的逾時的最大值。 預設值是 0。  
  
 這些是 SQL Server 執行個體的特定設定，而且應該建立在下列登錄機碼底下：  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL server\mssql<\<**版本**>。\<*instance_name*> \XATimeout  
  
> [!NOTE]  
>  在 64 位元機器中執行的 32 位元 SQL Server，登錄設定應建立下列機碼下： HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL server\mssql<\<版本 >。 < instance_name > \XATimeout  
  
 如果逾時到期，當此設定已啟動且交易已由 SQL Server 回復時，會設定每一筆交易的逾時值。 根據這些登錄設定，並根據使用者已透過 XAResource.setTransactionTimeout() 指定的設定，來決定此逾時。 這些逾時值解譯方式的幾個範例，如下所示：  
  
-   XADefaultTimeout = 0、XAMaxTimeout = 0  
  
     表示不使用預設的逾時，在用戶端上將不強制執行最大逾時。 在此情況下，只有當用戶端使用 XAResource.setTransactionTimeout 設定逾時，此交易才會有逾時。  
  
-   XADefaultTimeout = 60、XAMaxTimeout = 0  
  
     表示如果用戶端未指定任何逾時，則所有交易都會都有 60 秒逾時。 如果用戶端指定了逾時，則會使用該逾時值。 不會強制執行逾時最大值。  
  
-   XADefaultTimeout = 30、XAMaxTimeout = 60  
  
     表示如果用戶端未指定任何逾時，則所有交易都會都有 30 秒逾時。 如果用戶端指定了任何逾時，則只要是少於 60 秒 (最大值)，就會使用用戶端的逾時。  
  
-   XADefaultTimeout = 0、XAMaxTimeout = 30  
  
     表示如果用戶端未指定任何逾時，則所有交易都會都有 30 秒逾時 (最大值)。 如果用戶端指定了任何逾時，則只要是少於 30 秒 (最大值)，就會使用用戶端的逾時。  
  
### <a name="upgrading-sqljdbcxadll"></a>升級 sqljdbc_xa.dll  
 當您安裝新版 JDBC 驅動程式時，也應該使用新版的 sqljdbc_xa.dll 來升級伺服器上的 sqljdbc_xa.dll。  
  
> [!IMPORTANT]  
>  您應該在維護時段或者沒有任何 MS DTC 交易正在進行時升級 sqljdbc_xa.dll。  
  
1.  卸載 sqljdbc_xa.dll 使用[!INCLUDE[tsql](../../includes/tsql_md.md)]命令**DBCC sqljdbc_xa (FREE)**。  
  
2.  將新的 sqljdbc_xa.dll 從 JDBC 驅動程式安裝目錄複製到 Binn 目錄的每個[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]電腦中會參與分散式交易。  
  
     當系統呼叫 sqljdbc_xa.dll 中的擴充程序時，就會載入新的 DLL。 您不需要重新啟動[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]以載入新的定義。  
  
### <a name="configuring-the-user-defined-roles"></a>設定使用者定義角色  
 若要授與權限給特定使用者以使用 JDBC Driver 參與分散式交易，請將該使用者新增至 SqlJDBCXAUser 角色。 例如，使用下列[!INCLUDE[tsql](../../includes/tsql_md.md)]程式碼以使用者名稱為 'shelby' （SQL 標準登入使用者名稱為 'shelby'） 加入至 SqlJDBCXAUser 角色：  
  
```  
USE master  
GO  
EXEC sp_grantdbaccess 'shelby', 'shelby'  
GO  
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelby'  
```  
  
 每一個資料庫都會定義 SQL 使用者自訂角色。 若要基於安全目的來建立您自己的角色，您將必須在每一個資料庫中定義角色，然後在每一個資料庫中新增使用者。 SqlJDBCXAUser 角色一定是定義在 master 資料庫中，因為它是用來授與存取 SQL JDBC 擴充預存程序 (位於 master 資料庫) 的權限。 您必須先授與個別使用者存取 master 的權限，然後在您登入 master 資料庫時，再授與他們存取 SqlJDBCXAUser 角色的權限。  
  
## <a name="example"></a>範例  
  
```  
import java.net.Inet4Address;  
import java.sql.*;  
import java.util.Random;  
import javax.transaction.xa.*;  
import javax.sql.*;  
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
      String connectionUrl = prefix + serverName + ":" + portNumber  
         + ";databaseName=" + databaseName + ";user=" + user + ";password=" + password;  
  
      try {  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         Connection con = DriverManager.getConnection(connectionUrl);  
  
         // Create a test table.  
         Statement stmt = con.createStatement();  
         try {  
            stmt.executeUpdate("DROP TABLE XAMin");   
         }  
         catch (Exception e) {  
         }  
         stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");  
         stmt.close();  
         con.close();  
  
         // Create the XA data source and XA ready connection.  
         SQLServerXADataSource ds = new SQLServerXADataSource();  
         ds.setUser(user);  
         ds.setPassword(password);  
         ds.setServerName(serverName);  
         ds.setPortNumber(portNumber);  
         ds.setDatabaseName(databaseName);  
         XAConnection xaCon = ds.getXAConnection();  
         con = xaCon.getConnection();  
  
         // Get a unique Xid object for testing.  
         XAResource xaRes = null;  
         Xid xid = null;  
         xid = XidImpl.getUniqueXid(1);  
  
         // Get the XAResource object and set the timeout value.  
         xaRes = xaCon.getXAResource();  
         xaRes.setTransactionTimeout(0);  
  
         // Perform the XA transaction.  
         System.out.println("Write -> xid = " + xid.toString());  
         xaRes.start(xid,XAResource.TMNOFLAGS);  
         PreparedStatement pstmt =   
         con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");  
         pstmt.setInt(1,1);  
         pstmt.setString(2,xid.toString());  
         pstmt.executeUpdate();  
  
         // Commit the transaction.  
         xaRes.end(xid,XAResource.TMSUCCESS);  
         xaRes.commit(xid,true);  
  
         // Cleanup.  
         con.close();  
         xaCon.close();  
  
         // Open a new connection and read back the record to verify that it worked.  
         con = DriverManager.getConnection(connectionUrl);  
         ResultSet rs = con.createStatement().executeQuery("SELECT * FROM XAMin");  
         rs.next();  
         System.out.println("Read -> xid = " + rs.getString(2));  
         rs.close();  
         con.close();  
      }   
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
  
class XidImpl implements Xid {  
  
   public int formatId;  
   public byte[] gtrid;  
   public byte[] bqual;  
   public byte[] getGlobalTransactionId() {return gtrid;}  
   public byte[] getBranchQualifier() {return bqual;}  
   public int getFormatId() {return formatId;}  
  
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
      for (int i=0; i<gtrid.length; i++) {  
         hexVal = gtrid[i]&0xFF;  
         if ( hexVal < 0x10 )  
            sb.append("0" + Integer.toHexString(gtrid[i]&0xFF));  
         else  
            sb.append(Integer.toHexString(gtrid[i]&0xFF));  
         }  
         sb.append("} bqual(" + bqual.length + ")={0x");  
         for (int i=0; i<bqual.length; i++) {  
            hexVal = bqual[i]&0xFF;  
            if ( hexVal < 0x10 )  
               sb.append("0" + Integer.toHexString(bqual[i]&0xFF));  
            else  
               sb.append(Integer.toHexString(bqual[i]&0xFF));  
         }  
         sb.append("}");  
         return sb.toString();  
      }  
  
      // Returns a globally unique transaction id.  
      static byte [] localIP = null;  
      static int txnUniqueID = 0;  
      static Xid getUniqueXid(int tid) {  
  
      Random rnd = new Random(System.currentTimeMillis());  
      txnUniqueID++;  
      int txnUID = txnUniqueID;  
      int tidID = tid;  
      int randID = rnd.nextInt();  
      byte[] gtrid = new byte[64];  
      byte[] bqual = new byte[64];  
      if ( null == localIP) {  
         try {  
            localIP = Inet4Address.getLocalHost().getAddress();  
         }  
         catch ( Exception ex ) {  
            localIP =  new byte[] { 0x01,0x02,0x03,0x04 };  
         }  
      }  
      System.arraycopy(localIP,0,gtrid,0,4);  
      System.arraycopy(localIP,0,bqual,0,4);  
  
      // Bytes 4 -> 7 - unique transaction id.  
      // Bytes 8 ->11 - thread id.  
      // Bytes 12->15 - random number generated by using seed from current time in milliseconds.  
      for (int i=0; i<=3; i++) {  
         gtrid[i+4] = (byte)(txnUID%0x100);  
         bqual[i+4] = (byte)(txnUID%0x100);  
         txnUID >>= 8;  
         gtrid[i+8] = (byte)(tidID%0x100);  
         bqual[i+8] = (byte)(tidID%0x100);  
         tidID >>= 8;  
         gtrid[i+12] = (byte)(randID%0x100);  
         bqual[i+12] = (byte)(randID%0x100);  
         randID >>= 8;  
      }  
      return new XidImpl(0x1234, gtrid, bqual);  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 JDBC Driver 執行交易](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
