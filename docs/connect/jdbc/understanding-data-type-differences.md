---
title: 了解資料類型差異 |Microsoft 文件
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
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cf10944059322a159de43ccee2a7e4d8ed1d8526
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="understanding-data-type-differences"></a>了解資料類型差異
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  有許多的 Java 程式語言資料類型之間的差異和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]協助調解這些差異，透過各種類型的轉換。  
  
## <a name="character-types"></a>字元類型  
 JDBC 字元字串資料類型為**CHAR**， **VARCHAR**，和**LONGVARCHAR**。 JDBC 驅動程式提供 JDBC 4.0 API 的支援。 在 JDBC 4.0 中，JDBC 字元字串資料類型也可以是**NCHAR**， **NVARCHAR**，和**LONGNVARCHAR**。 這些新的字元字串類型會以 Unicode 格式維護 Java 原生字元類型，並且移除執行任何 ANSI-to-Unicode 或 Unicode-to-ANSI 轉換的需求。  
  
|型別|Description|  
|----------|-----------------|  
|Fixed-length|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Char**和**nchar**資料類型會直接對應到 JDBC **CHAR**和**NCHAR**型別。 這些是當資料行具有 SET ANSI_PADDING ON 時，會由伺服器提供填補的固定長度類型。 永遠開啟填補**nchar**，但針對**char**，其中伺服器 char 資料行未開啟填補時的情況下，JDBC 驅動程式會加入填補。|  
|Variable-length|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Varchar**和**nvarchar**類型會直接對應到 JDBC **VARCHAR**和**NVARCHAR**類型，分別。|  
|長整數|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**文字**和**ntext**類型會對應到 JDBC **LONGVARCHAR**和**LONGNVARCHAR**分別輸入。 這些是已被取代的類型從[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]，因此您應該改用大數值類型， **varchar （max)** 或**nvarchar （max)** 請改用。<br /><br /> 使用 update\<數值類型 > 和[updateObject （int，java.lang.Object）](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md)方法會失敗**文字**和**ntext**伺服器資料行。 不過，使用[setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)支援對具有指定的字元轉換類型的方法**文字**和**ntext**伺服器資料行。|  
  
## <a name="binary-string-types"></a>二進位字串類型  
 JDBC 二進位字串類型為**二進位**， **VARBINARY**，和**LONGVARBINARY**。  
  
|型別|Description|  
|----------|-----------------|  
|Fixed-length|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**二進位**輸入都會直接對應到 JDBC**二進位**型別。 這是當資料行具有 SET ANSI_PADDING ON 時，會由伺服器提供填補的固定長度類型。 當伺服器 char 資料行未開啟填補時，JDBC 驅動程式會加入填補。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**時間戳記**型別是 JDBC**二進位**具有 8 個位元組的固定長度類型。|  
|Variable-length|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Varbinary**類型會對應到 JDBC **VARBINARY**型別。<br /><br /> **Udt**輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]對應至為 JDBC **VARBINARY**型別。|  
|長整數|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**映像**類型會對應到 JDBC **LONGVARBINARY**型別。 此類型已被取代，從[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]，因此您應該改用大數值型別**varbinary （max)** 改為。|  
  
## <a name="exact-numeric-types"></a>精確數值類型  
 JDBC 精確數值類型會直接對應到其相對應的 SQL Server 類型。  
  
|型別|Description|  
|----------|-----------------|  
|BIT|JDBC**元**類型代表單一位元，可以是 0 或 1。 這會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**元**型別。|  
|TINYINT|JDBC **TINYINT**類型代表單一位元組。 這會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **tinyint**型別。|  
|SMALLINT|JDBC **SMALLINT**類型代表帶正負號的 16 位元整數。 這會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **smallint**型別。|  
|INTEGER|JDBC**整數**類型代表帶正負號的 32 位元整數。 這會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **int**型別。|  
|bigint|JDBC **BIGINT**類型代表帶正負號的 64 位元整數。 這會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **bigint**型別。|  
|NUMERIC|JDBC**數值**類型代表固定有效位數的十進位值，會保留相同的有效位數的值。 **數值**類型會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**數值**型別。|  
|DECIMAL|JDBC**十進位**類型代表固定有效位數的十進位值，保留值的最少為指定的有效位數。 **十進位**類型會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**十進位**型別。<br /><br /> JDBC**十進位**類型也會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **money**和**smallmoney**類型，也就是儲存在 8 和 4 中特定固定有效位數 decimal 類型位元組，分別。|  
  
## <a name="approximate-numeric-types"></a>近似數值類型  
 JDBC 近似數值類型為**真實**， **DOUBLE**，和**FLOAT**。  
  
|型別|Description|  
|----------|-----------------|  
|REAL|JDBC**真實**類型具有 7 個位數的有效位數 （單精確度），並會直接對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**真實**型別。|  
|DOUBLE|JDBC **DOUBLE**類型具有 15 位數的有效位數 （雙精確度），並將對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **float**型別。 JDBC **FLOAT**類型是同義字的**DOUBLE**。 因為可能會混淆**FLOAT**和**DOUBLE**， **DOUBLE**偏好。|  
  
## <a name="datetime-types"></a>日期時間類型  
 JDBC**時間戳記**類型會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime**和**smalldatetime**型別。 **Datetime**類型會儲存在兩個 4 位元組整數。 **Smalldatetime**類型會保留相同的資訊 （日期和時間），但較不精確，在兩個 2 位元組的小整數。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**時間戳記**類型是固定長度二進位字串類型。 它不會對應到任何的 JDBC 時間類型：**日期**，**時間**，或**時間戳記**。  
  
## <a name="custom-type-mapping"></a>自訂類型對應  
 JDBC sql 資料介面用於 JDBC 自訂類型對應功能進階類型 （Udt、 Struct 等）。 而 JDBC 驅動程式中並未實作此功能。  
  
## <a name="see-also"></a>另請參閱  
 [了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
