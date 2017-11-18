---
title: "使用資料庫鏡像 (JDBC) |Microsoft 文件"
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
ms.assetid: 4ff59218-0d3b-4274-b647-9839c4955865
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cdc263be0e8283ed1d71630a61f4e3d60406edc8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="using-database-mirroring-jdbc"></a>使用資料庫鏡像 (JDBC)
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  資料庫鏡像主要是一種用於增加資料庫可用性及資料備用性的軟體解決方案。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供對資料庫鏡像的隱含支援，以便開發人員不需要撰寫任何程式碼或採取其他任何動作，當它已設定資料庫。  
  
 資料庫鏡像，是根據每個資料庫來實作時，會保留一份[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]待命伺服器上的實際執行資料庫。 此伺服器為熱或暖待命伺服器，端視資料庫鏡像工作階段的組態和狀態而定。 熱待命伺服器支援迅速容錯移轉，不會失去已認可的交易，而暖待命伺服器則支援強制服務 (可能會失去資料)。  
  
 生產資料庫稱為*主體*資料庫，而待命副本稱為*鏡像*資料庫。 主體資料庫和鏡像資料庫必須位於不同的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]（伺服器執行個體），而且如果可能的話，它們應該位於個別的電腦上。  
  
 生產伺服器執行個體 (稱為主體伺服器) 會與待命伺服器執行個體 (稱為鏡像伺服器) 通訊。 主體伺服器及鏡像伺服器在資料庫鏡像工作階段內會是夥伴。 如果主體伺服器失敗，鏡像伺服器可以讓其資料庫成為主體資料庫稱為程序，透過*容錯移轉*。 例如，Partner_A 與 Partner_B 是兩個夥伴伺服器，其中主體資料庫一開始位於 Partner_A 上做為主體伺服器，而鏡像資料庫位於 Partner_B 上做為鏡像伺服器。 如果 Partner_A 離線，Partner_B 上的資料庫可以容錯移轉，變成目前的主體資料庫。 當 Partner_A 重新加入鏡像工作階段時，它會變成鏡像伺服器而其資料庫會變成鏡像資料庫。  
  
 如果 Partner_A 伺服器遭到不能修理的損壞，則可將 Partner_C 伺服器連線，以充當 Partner_B (現在是主體伺服器) 的鏡像伺服器。 然而，在此案例中，用戶端應用程式必須包括程式設計邏輯，以確定會以資料庫鏡像組態中使用的新伺服器名稱，更新連接字串屬性。 否則，伺服器的連接可能會失敗。  
  
 替代的資料庫鏡像組態提供不同層次的效能及資料安全，並支援不同形式的容錯移轉。 如需詳細資訊，請參閱 「 資料庫鏡像概觀 >[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
## <a name="programming-considerations"></a>程式設計考量  
 當主體資料庫伺服器失敗時，用戶端應用程式會在回應 API 呼叫時收到錯誤，這表示與資料庫的連接已經中斷。 當發生這種情況時，將失去任何未認可的資料庫變更，而且將回復目前的交易。 如果發生這種情況，應用程式應該關閉連接 (或釋出資料來源物件)，然後嘗試重新開啟它。 連接時，新的連接會以透明方式重新導向至鏡像資料庫 (現在是作為主體伺服器)，而且用戶端不需修改連接字串或資料來源物件。  
  
 在最初建立連接時，主體伺服器會將其容錯移轉夥伴的身分，傳送給發生容錯移轉時將使用的用戶端。 當應用程式嘗試與失敗的主體伺服器建立初始連接時，用戶端並不知道容錯移轉夥伴的身分。 若要允許用戶端有機會處理此案例，failoverPartner 連接字串屬性，並選擇性地[setFailoverPartner](../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)資料來源方法，可讓用戶端指定的容錯移轉的身分識別夥伴本身。 此用戶端屬性只會在此案例中使用；如果主體伺服器可用，就不會使用。  
  
> [!NOTE]  
>  在連接字串中或利用資料來源物件指定 failoverPartner 時，也必須設定 databaseName 屬性，否則將擲回例外狀況。 如果未明確指定 failoverPartner 和 databaseName，當主體資料庫伺服器失敗時，應用程式將不會嘗試容錯移轉。 換句話說，透明的重新導向僅適用於明確指定 failoverPartner 和 databaseName 的連接。 如需 failoverPartner 及其他連接字串屬性的詳細資訊，請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 如果用戶端所提供的容錯移轉夥伴伺服器並未參照當做指定資料庫之容錯移轉夥伴的伺服器，而且如果所參照的伺服器/資料庫處於鏡像排列中，伺服器會拒絕連接。 雖然[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)類別提供[getFailoverPartner](../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)方法，這個方法只會傳回連接字串中指定的容錯移轉夥伴名稱或setFailoverPartner 方法。 若要擷取目前正在使用的實際的容錯移轉夥伴名稱，請使用下列[!INCLUDE[tsql](../../includes/tsql_md.md)]陳述式：  
  
```  
SELECT m.mirroring_role_DESC, m.mirroring_state_DESC,  
m.mirroring_partner_instance FROM sys.databases as db,  
sys.database_mirroring AS m WHERE db.name = 'MirroringDBName'  
AND db.database_id = m.database_id  
```  
  
> [!NOTE]  
>  您需要變更此陳述式，以使用您的鏡像資料庫名稱。  
  
 您應該考慮快取夥伴資訊以更新連接字串，或設計如果第一次嘗試建立連接失敗時要進行的重試策略。  
  
## <a name="example"></a>範例  
 在下列範例中，第一次會嘗試連接至主體伺服器。 如果失敗並發生例外狀況，則會嘗試連接至鏡像伺服器 (鏡像伺服器可能已升級為新的主體伺服器)。 請注意，連接字串中有使用 failoverPartner 屬性。  
  
```  
import java.sql.*;  
  
public class clientFailover {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://serverA:1433;" +  
         "databaseName=AdventureWorks;integratedSecurity=true;" +  
         "failoverPartner=serverB";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
  
      try {  
         // Establish the connection to the principal server.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         System.out.println("Connected to the principal server.");  
  
         // Note that if a failover of serverA occurs here, then an  
         // exception will be thrown and the failover partner will  
         // be used in the first catch block below.  
  
         // Create and execute an SQL statement that inserts some data.  
         stmt = con.createStatement();  
  
         // Note that the following statement assumes that the   
         // TestTable table has been created in the AdventureWorks  
         // sample database.  
         stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");  
      }  
  
      // Handle any errors that may have occurred.  
      catch (SQLException se) {  
         try {  
            // The connection to the principal server failed,  
            // try the mirror server which may now be the new  
            // principal server.  
            System.out.println("Connection to principal server failed, " +  
            "trying the mirror server.");  
            con = DriverManager.getConnection(connectionUrl);  
            System.out.println("Connected to the new principal server.");  
            stmt = con.createStatement();  
            stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");  
         }  
         catch (Exception e) {  
            e.printStackTrace();  
         }  
      }  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      // Close the JDBC objects.  
      finally {  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [連接到 SQL Server JDBC 驅動程式](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

