---
title: 了解資料類型轉換 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98fa7488-aac3-45b4-8aa4-83ed6ab638b4
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e18bd56e110cccab17488de752ba5ab4c8666fa9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="understanding-data-type-conversions"></a>了解資料類型轉換
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  為了順利將 Java 程式語言資料類型的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供 JDBC 規格所需的資料類型轉換。 增加更多彈性，為所有類型都是來回轉換**物件**，**字串**，和**byte []** 資料型別。  
  
## <a name="getter-method-conversions"></a>Getter 方法轉換  
 根據[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別，下列圖表包含 JDBC 驅動程式轉換對應 get\<類型 > （） 方法的[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)類別，而 get支援的轉換\<型別 > 方法的[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別。  
  
 ![JDBCGetterConversions](../../connect/jdbc/media/jdbcgetterconversions.gif "JDBCGetterConversions")  
  
 JDBC Driver 的 getter 方法所支援的轉換有三種類別：  
  
-   **不失真 (x)**： 轉換的情況，getter 類型相同或小於基礎伺服器類型。 例如，在基礎伺服器十進位資料行上呼叫 getBigDecimal，不不需要任何轉換。  
  
-   **轉換 (y)**： 從數值伺服器類型轉換為 Java 語言類型，其中是一般轉換並會遵循 Java 語言轉換規則。 針對這些轉換，一定會截斷有效位數 (絕對不會進位)，而溢位則會當做目的地類型的模數來處理 (也就是較小)。 例如，在基礎呼叫 getInt**十進位**含有"1.9999"的資料行將會傳回"1"，或如果基礎**十進位**值是"3000000000"則**int**值會溢位為"-1294967296"。  
  
-   **視資料而定 (z)**： 從基礎字元類型到數值類型的轉換，需要字元類型值包含可轉換為該類型。 不會執行其他轉換。 如果該值對於 getter 類型來說太大，則該值無效。 例如，如果 getInt 含有"53"在 varchar （50） 資料行上呼叫時，會傳回值為**int**; 但如果基礎值為"xyz"或"3000000000"，會擲回錯誤。  
  
 如果在上呼叫 getString**二進位**， **varbinary**， **varbinary （max)**，或**映像**資料行資料類型，則會傳回值為十六進位字串值。  
  
## <a name="updater-method-conversions"></a>Updater 方法轉換  
 使用 Java 類型資料傳遞給更新\<類型 > （） 方法的[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)類別，則適用下列轉換。  
  
 ![JDBCUpdaterConversions](../../connect/jdbc/media/jdbc_jdbcupdatterconversions.gif "JDBCUpdaterConversions")  
  
 JDBC Driver 的 updater 方法所支援的轉換有三種類別：  
  
-   **不失真 (x)**： 轉換的情況，updater 類型相同或小於基礎伺服器類型。 例如，在基礎伺服器十進位資料行上呼叫 updateBigDecimal 時，不需要轉換。  
  
-   **轉換 (y)**： 從數值伺服器類型轉換為 Java 語言類型，其中是一般轉換並會遵循 Java 語言轉換規則。 針對這些轉換，一定會截斷有效位數 (絕對不會進位)，而溢位則會當做目的地 (較小) 類型的模數來處理。 例如，在基礎呼叫 updateDecimal **int**含有"1.9999"的資料行將會傳回"1"，或如果基礎**十進位**值是"3000000000"則**int**值溢位為"-1294967296"。  
  
-   **視資料而定 (z)**： 從基礎來源資料類型轉換為目的地資料類型需要包含的值可轉換為目的地類型。 不會執行其他轉換。 如果該值對於 getter 類型來說太大，則該值無效。 例如，如果在含有 "53" 的 int 資料行上呼叫 updateString，更新會成功；但如果基礎字串值為 "foo" 或 "3000000000"，則會擲回錯誤。  
  
 當上呼叫 updateString**二進位**， **varbinary**， **varbinary （max)**，或**映像**資料行資料類型，它會處理的字串值以十六進位字串值。  
  
 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料行資料類型是**XML**，資料值必須是有效**XML**。 呼叫 updateBytes、 updateBinaryStream、 或 updateBlob 方法時，此資料值應該是 XML 字元的十六進位字串表示。 例如：  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 請注意，如果 XML 字元採用特定字元編碼，就需要位元組順序標示 (BOM)。  
  
## <a name="setter-method-conversions"></a>Setter 方法轉換  
 使用 Java 類型資料集傳遞\<類型 > （） 方法的[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)類別和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別，則適用下列轉換。  
  
 ![JDBCSetterConversions](../../connect/jdbc/media/jdbc_jdbcsetterconversions_v2.gif "JDBCSetterConversions")  
  
 伺服器會嘗試任何一種轉換，並會在發生失敗時傳回錯誤。  
  
 如果是**字串**資料型別，如果值超出的長度**VARCHAR**，則會對應至**LONGVARCHAR**。 同樣地， **NVARCHAR**對應至**LONGNVARCHAR**如果值超出的支援的長度**NVARCHAR**。 同樣適用於**byte []**。 值長度超過**VARBINARY**變成**LONGVARBINARY**。  
  
 JDBC Driver 的 setter 方法所支援的轉換有兩種類別：  
  
-   **不失真 (x)**： 轉換的數值情況，setter 類型相同或小於基礎伺服器類型。 例如，當基礎的伺服器上呼叫 setBigDecimal**十進位**資料行，不需要任何轉換。 針對數值到字元的情況下，Java**數值**資料類型轉換成**字串**。 例如，呼叫 setDouble 值"53"在 varchar （50） 資料行上會產生該目的地資料行中的字元值"53"。  
  
-   **轉換 (y)**： 從 Java 轉換**數值**基礎伺服器類型**數值**較小的類型。 這是轉換規則並遵循[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]轉換慣例。 有效位數一律會截斷 (絕不進位)，而溢位則會擲回未支援的轉換錯誤。 例如，使用值為"1.9999"，"1"在目的地資料行中; 在基礎整數資料行結果的 updateDecimal但是，如果傳遞"3000000000"，驅動程式會擲回錯誤。  
  
-   **視資料而定 (z)**： 從 Java 轉換**字串**基礎類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別取決於下列條件： 驅動程式會傳送**字串**的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行轉換，如有必要。 如果 sendStringParametersAsUnicode 設定為 true 而且基礎[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料類型是**映像**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不允許將轉換**nvarchar**至**映像**並擲回 SQLServerException。 如果 sendStringParametersAsUnicode 設定為 false 而且基礎[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料類型是**映像**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]允許將轉換**varchar**至**映像**並不會擲回例外狀況。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 會執行轉換，並將錯誤傳遞回 JDBC 驅動程式發生問題時。  
  
 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料行資料類型是**XML**，資料值必須是有效**XML**。 呼叫 updateBytes、 updateBinaryStream、 或 updateBlob 方法時，此資料值應該是 XML 字元的十六進位字串表示。 例如：  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 請注意，如果 XML 字元採用特定字元編碼，就需要位元組順序標示 (BOM)。  
  
## <a name="conversions-on-setobject"></a>setObject 的轉換  
  
> [!NOTE]  
>  Microsoft JDBC Drivers 4.2 （和更新版本） for SQL Server 支援 JDBC 4.1 和 4.2。 如需在 4.1 和 4.2 資料型別對應和轉換的詳細資訊，請參閱[JDBC 驅動程式的 JDBC 4.1 相容性](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)和[JDBC 驅動程式的 JDBC 4.2 相容性](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)，除了以下資訊。  
  
 使用 Java 類型資料傳送至 setObject (\<類型 >) 的方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)類別，則適用下列轉換。  
  
 ![JDBCSetObjectConversions](../../connect/jdbc/media/jdbc_jdbcsetobjectconversions.gif "JDBCSetObjectConversions")  
  
 未指定的目標類型的 setObject 方法會使用預設對應。 如果是**字串**資料型別，如果值超出的長度**VARCHAR**，則會對應至**LONGVARCHAR**。 同樣地， **NVARCHAR**對應至**LONGNVARCHAR**如果值超出的支援的長度**NVARCHAR**。 同樣適用於**byte []**。 值長度超過**VARBINARY**變成**LONGVARBINARY**。  
  
 JDBC Driver 的 setObject 方法所支援的轉換有三種類別：  
  
-   **不失真 (x)**： 轉換的數值情況，setter 類型相同或小於基礎伺服器類型。 例如，當基礎的伺服器上呼叫 setBigDecimal**十進位**資料行，不需要任何轉換。 針對數值到字元的情況下，Java**數值**資料類型轉換成**字串**。 例如，呼叫 setDouble 值"53"在 varchar （50） 資料行上，將會產生該目的地資料行中的字元值"53"。  
  
-   **轉換 (y)**： 從 Java 轉換**數值**基礎伺服器類型**數值**較小的類型。 這是轉換規則並遵循[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]轉換慣例。 有效位數一律會截斷 (絕不進位)，而溢位則會擲出未支援的轉換錯誤。 例如，使用值為"1.9999"，"1"在目的地資料行中; 在基礎整數資料行結果的 updateDecimal但是，如果傳遞"3000000000"，驅動程式會擲回錯誤。  
  
-   **視資料而定 (z)**： 從 Java 轉換**字串**基礎類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別取決於下列條件： 驅動程式會傳送**字串**的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行轉換，如有必要。 如果 sendStringParametersAsUnicode 連接屬性設定為 true 而且基礎[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料類型是**映像**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不允許將轉換**nvarchar**至**映像**並擲回 SQLServerException。 如果 sendStringParametersAsUnicode 設定為 false 而且基礎[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料類型是**映像**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]允許將轉換**varchar**至**映像**並不會擲回例外狀況。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 會執行大量 set 轉換，並將錯誤傳遞回 JDBC 驅動程式發生問題時。 用戶端轉換是例外，而且只是不會執行**日期**，**時間**，**時間戳記**，**布林**，和**字串**值。  
  
 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料行資料類型是**XML**，資料值必須是有效**XML**。 呼叫 setObject(byte[], SQLXML)、setObject(inputStream, SQLXML) 或 setObject(Blob, SQLXML) 方法時，此資料值應該是 XML 字元的十六進位字串表示法。 例如：  
  
```  
<hello>world</hello> = 0x3C68656C6C6F3E776F726C643C2F68656C6C6F3E   
```  
  
 請注意，如果 XML 字元採用特定字元編碼，就需要位元組順序標示 (BOM)。  
  
## <a name="see-also"></a>另請參閱  
 [了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
