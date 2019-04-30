---
title: 有關用戶端使用 GEOMETRY、 GEOGRAPHY 和 HIERARCHYID 的警告 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 500ee6b3-2154-45d2-a3cf-8760166d9413
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 08b853d57068121fccb4db2341754eea0af7f734
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185864"
---
# <a name="warning-about-client-side-usage-of-geometry-geography-and-hierarchyid"></a>有關用戶端使用 GEOMETRY、GEOGRAPHY 和 HIERARCHYID 的警告
  組件**Microsoft.SqlServer.Types.dll**，其中包含空間資料類型，具有已從 10.0 版升級為 11.0 版。 當某些條件成立時，參考這個組件的自訂應用程式可能會失敗。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 組件**Microsoft.SqlServer.Types.dll**，其中包含空間資料類型，具有已從 10.0 版升級為 11.0 版。 當下列條件成立時，參考這個組件的自訂應用程式可能會失敗。  
  
-   當您移動自訂的應用程式從電腦所在[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]所在的電腦只安裝[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]是安裝，應用程式會失敗，因為參考的 10.0 版**SqlTypes**組件不存在。 您可能會收到下列錯誤訊息：`"Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified."`  
  
-   當您參考**SqlTypes**組件 11.0 版，也安裝了 10.0 版，您可能會看到此錯誤訊息： `"System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'."`  
  
-   當您參考**SqlTypes**組件 11.0 版從以.NET 3.5、 4 或 4.5 為目標的自訂應用程式，應用程式會失敗，因為 SqlClient 依照設計載入的組件 10.0 版。 當應用程式呼叫下列其中一個方法時，就會發生這項失敗：  
  
    -   `GetValue` 類別的 `SqlDataReader` 方法  
  
    -   `GetValues` 類別的 `SqlDataReader` 方法  
  
    -   `SqlDataReader` 類別的括號索引運算子 []  
  
    -   `ExecuteScalar` 類別的 `SqlCommand` 方法  
  
## <a name="corrective-action"></a>更正動作  
 您可以使用下列其中一個方法來解決這個問題：  
  
-   您可以在程式碼中呼叫 `GetSqlBytes` 方法 (而非上列 Get 方法) 來擷取 CLR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統類型，藉以解決此問題，如下列範例所示：  
  
    ```csharp  
    string query = "SELECT [SpatialColumn] FROM [SpatialTable]";  
          using (SqlConnection conn = new SqlConnection("..."))  
          {  
                SqlCommand cmd = new SqlCommand(query, conn);  
  
                conn.Open();  
                SqlDataReader reader = cmd.ExecuteReader();  
  
                while (reader.Read())  
                {  
                      // In version 11.0 only  
                      SqlGeometry g =   
    SqlGeometry.Deserialize(reader.GetSqlBytes(0));  
  
                      // In version 10.0 or 11.0  
                      SqlGeometry g2 = new SqlGeometry();  
                      g.Read(new BinaryReader(reader.GetSqlBytes(0).Stream));  
                }  
          }  
    ```  
  
-   您可以在應用程式組態檔中使用組件重新導向，藉以解決此問題，如下列範例所示：  
  
    ```xml  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        ...  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.SqlServer.Types" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="10.0.0.0" newVersion="11.0.0.0" />  
        </dependentAssembly>  
        ...  
    </assemblyBinding>  
    ```  
  
-   您可以在連接字串中針對 "Type System Version" 屬性指定 "SQL Server 2012" 值，強制 SqlClient 載入組件 11.0 版，藉以解決此問題。 此連接字串屬性僅適用於 .NET 4.5 和更新版本。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md
)  
  
  
