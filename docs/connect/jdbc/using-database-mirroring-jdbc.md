---
title: 使用資料庫鏡像 (JDBC) | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4ff59218-0d3b-4274-b647-9839c4955865
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0de521e6ef913d27a020cc76f1dc6de00d0f409
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026429"
---
# <a name="using-database-mirroring-jdbc"></a>使用資料庫鏡像 (JDBC)

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

資料庫鏡像主要是一種用於增加資料庫可用性及資料備用性的軟體解決方案。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供隱含的資料庫鏡像支援，所以在對資料庫設定資料庫鏡像時，開發人員不需撰寫任何程式碼或採取任何其他動作。

資料庫鏡像是根據每一個資料庫來實作，它會在待命伺服器上保留 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生產資料庫的複本。 此伺服器為熱或暖待命伺服器，端視資料庫鏡像工作階段的組態和狀態而定。 熱待命伺服器支援迅速容錯移轉，不會失去已認可的交易，而暖待命伺服器則支援強制服務 (可能會失去資料)。

生產資料庫稱為「主體」  資料庫，而待命複本則稱為「鏡像」  資料庫。 主體資料庫和鏡像資料庫必須位於個別的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (伺服器執行個體)，而且它們應該位於個別的電腦上 (如果可能的話)。

生產伺服器執行個體 (稱為主體伺服器) 會與待命伺服器執行個體 (稱為鏡像伺服器) 通訊。 主體伺服器及鏡像伺服器在資料庫鏡像工作階段內會是夥伴。 如果主體伺服器失敗，則鏡像伺服器可以透過稱為「容錯移轉」  的處理序，使鏡像伺服器的資料庫成為主體資料庫。 例如，Partner_A 與 Partner_B 是兩個夥伴伺服器，其中主體資料庫一開始位於 Partner_A 上做為主體伺服器，而鏡像資料庫位於 Partner_B 上做為鏡像伺服器。 如果 Partner_A 離線，Partner_B 上的資料庫可以容錯移轉，變成目前的主體資料庫。 當 Partner_A 重新加入鏡像工作階段時，它會變成鏡像伺服器而其資料庫會變成鏡像資料庫。

如果 Partner_A 伺服器遭到不能修理的損壞，則可將 Partner_C 伺服器連線，以充當 Partner_B (現在是主體伺服器) 的鏡像伺服器。 然而，在此案例中，用戶端應用程式必須包括程式設計邏輯，以確定會以資料庫鏡像組態中使用的新伺服器名稱，更新連接字串屬性。 否則，伺服器的連接可能會失敗。

替代的資料庫鏡像組態提供不同層次的效能及資料安全，並支援不同形式的容錯移轉。 如需詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書中的＜資料庫鏡像概觀＞。

## <a name="programming-considerations"></a>程式設計考量

當主體資料庫伺服器失敗時，用戶端應用程式會在回應 API 呼叫時收到錯誤，這表示與資料庫的連接已經中斷。 當發生這種情況時，將失去任何未認可的資料庫變更，而且將回復目前的交易。 如果發生這種情況，應用程式應該關閉連接 (或釋出資料來源物件)，然後嘗試重新開啟它。 連接時，新的連接會以透明方式重新導向至鏡像資料庫 (現在是作為主體伺服器)，而且用戶端不需修改連接字串或資料來源物件。

在最初建立連接時，主體伺服器會將其容錯移轉夥伴的身分，傳送給發生容錯移轉時將使用的用戶端。 當應用程式嘗試與失敗的主體伺服器建立初始連接時，用戶端並不知道容錯移轉夥伴的身分。 若要讓用戶端有機會處理此案例，failoverPartner 連接字串屬性及選用的 [setFailoverPartner](../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) 資料來源方法，可讓用戶端指定自己的容錯移轉夥伴身分。 此用戶端屬性只會在此案例中使用；如果主體伺服器可用，就不會使用。

> [!NOTE]  
> 在連接字串中或利用資料來源物件指定 failoverPartner 時，也必須設定 databaseName 屬性，否則將擲回例外狀況。 如果未明確指定 failoverPartner 和 databaseName，當主體資料庫伺服器失敗時，應用程式將不會嘗試容錯移轉。 換句話說，透明的重新導向僅適用於明確指定 failoverPartner 和 databaseName 的連接。 如需 failoverPartner 及其他連接字串屬性的詳細資訊，請參閱[設定連線屬性](../../connect/jdbc/setting-the-connection-properties.md)。

如果用戶端所提供的容錯移轉夥伴伺服器並未參照當做指定資料庫之容錯移轉夥伴的伺服器，而且如果所參照的伺服器/資料庫處於鏡像排列中，伺服器會拒絕連接。 雖然 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 類別提供 [getFailoverPartner](../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md) 方法，但是此方法只會傳回連接字串或 setFailoverPartner 方法中所指定容錯移轉夥伴的名稱。 若要擷取目前正在使用之真正容錯移轉夥伴的名稱，請使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：

```sql
SELECT m.mirroring_role_DESC, m.mirroring_state_DESC,  
m.mirroring_partner_instance FROM sys.databases as db,  
sys.database_mirroring AS m WHERE db.name = 'MirroringDBName'  
AND db.database_id = m.database_id  
```

> [!NOTE]  
> 您需要變更此陳述式，以使用您的鏡像資料庫名稱。

您應該考慮快取夥伴資訊以更新連接字串，或設計如果第一次嘗試建立連接失敗時要進行的重試策略。

## <a name="example"></a>範例

在下列範例中，第一次會嘗試連接至主體伺服器。 如果失敗並發生例外狀況，則會嘗試連接至鏡像伺服器 (鏡像伺服器可能已升級為新的主體伺服器)。 請注意，連接字串中有使用 failoverPartner 屬性。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class ClientFailover {
    public static void main(String[] args) {

        String connectionUrl = "jdbc:sqlserver://serverA:1433;"
                + "databaseName=AdventureWorks;integratedSecurity=true;"
                + "failoverPartner=serverB";

        // Establish the connection to the principal server.
        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement();) {
            System.out.println("Connected to the principal server.");

            // Note that if a failover of serverA occurs here, then an
            // exception will be thrown and the failover partner will
            // be used in the first catch block below.

            // Execute a SQL statement that inserts some data.

            // Note that the following statement assumes that the
            // TestTable table has been created in the AdventureWorks
            // sample database.
            stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");
        }
        catch (SQLException se) {
            System.out.println("Connection to principal server failed, " + "trying the mirror server.");
            // The connection to the principal server failed,
            // try the mirror server which may now be the new
            // principal server.
            try (Connection con = DriverManager.getConnection(connectionUrl);
                    Statement stmt = con.createStatement();) {
                System.out.println("Connected to the new principal server.");
                stmt.executeUpdate("INSERT INTO TestTable (Col2, Col3) VALUES ('a', 10)");
            }
            // Handle any errors that may have occurred.
            catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## <a name="see-also"></a>另請參閱

[使用 JDBC 驅動程式連線到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
