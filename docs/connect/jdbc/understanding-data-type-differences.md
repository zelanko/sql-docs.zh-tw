---
title: 瞭解資料類型差異 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 906a4abf0768fcad2e5ac31a0ee93345dcc8b30c
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027386"
---
# <a name="understanding-data-type-differences"></a>了解資料類型差異

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Java 程式設計語言資料類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型之間，存在一些差異。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會透過各種類型的轉換，協助調解這些差異。  

## <a name="character-types"></a>字元類型

JDBC 字元字串資料類型為**CHAR**、 **VARCHAR**和**LONGVARCHAR**。 JDBC 驅動程式提供 JDBC 4.0 API 的支援。 在 JDBC 4.0 中, JDBC 字元字串資料類型也可以是**NCHAR**、 **NVARCHAR**和**LONGNVARCHAR**。 這些新的字元字串類型會以 Unicode 格式維護 Java 原生字元類型，並且移除執行任何 ANSI-to-Unicode 或 Unicode-to-ANSI 轉換的需求。  
  
| 類型            | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fixed-length    |     Char 和 Nchar 資料類型會直接對應到 JDBC char 和 Nchar 類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 這些是當資料行具有 `SET ANSI_PADDING ON` 時，由伺服器提供填補的固定長度類型。 **nchar** 一定會開啟填補；至於 **char**，當伺服器 char 資料行未開啟填補時，JDBC 驅動程式會新增填補。                                                                                                                                                                                                                                                                                                                                                                                      |
| Variable-length |     Varchar 和 Nvarchar 類型會分別對應到 JDBC Varchar 和 Nvarchar 類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 長整數            |     Text 和 Ntext 類型分別對應到 JDBC LONGVARCHAR 和 LONGNVARCHAR 類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 這些是從開始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的已淘汰類型, 因此您應該改用大數數值型別 ( **Varchar (max)** 或**Nvarchar (max))** 。<br /><br /> 針對**text**和\< **Ntext**伺服器資料行, 使用 update Numeric 類型 > 和[updateObject (int, java)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md)方法將會失敗。 不過，支援對 **text** 和 **ntext** 伺服器資料行使用 [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) 方法，並搭配指定的字元轉換類型。 |
  
## <a name="binary-string-types"></a>二進位字串類型

JDBC 二進位字串類型為**binary**、 **VARBINARY**和**LONGVARBINARY**。  
  
| 類型            | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Fixed-length    | 二進位類型會直接對應到 JDBC**二進位**類型。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 這是當資料行具有 SET ANSI_PADDING ON 時，會由伺服器提供填補的固定長度類型。 當伺服器 char 資料行未開啟填補時，JDBC 驅動程式會加入填補。<br /><br /> Timestamp 類型是固定長度為8個位元組的 JDBC**二進位**類型。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |
| Variable-length | Varbinary 類型會對應到 JDBC **Varbinary**類型。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> 中  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 udt 類型會對應到 JDBC 做為**VARBINARY**類型。                                                                                                                                                                                                                                 |
| 長整數            | 影像類型會對應到 JDBC **LONGVARBINARY**類型。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，這個類型已淘汰，因此您應該改用大數值類型 **varbinary(max)** 。                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>精確數值類型

JDBC 精確數值類型會直接對應到其相對應的 SQL Server 類型。  
  
| 類型     | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | JDBC **BIT** 類型代表可為 0 或 1 的單一位元。 這會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **位**類型。                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | JDBC **TINYINT** 類型代表單一位元組。 這會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Tinyint**型別。                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | JDBC **SMALLINT** 類型代表帶正負號的 16 位元整數。 這會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Smallint**類型。                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | JDBC **SMALLINT** 類型代表帶正負號的 32 位元整數。 這會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int**型別。                                                                                                                                                                                                                                                                                                                                           |
| bigint   | JDBC **BIGINT** 類型代表帶正負號的 64 位元整數。 這會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Bigint**類型。                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | JDBC **NUMERIC** 類型代表固定有效位數的十進位值，此值會保留相同的有效位數值。 **數值**類型會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **數值**類型。                                                                                                                                                                                                                                                                   |
| DECIMAL  | JDBC **DECIMAL** 類型代表固定有效位數的十進位值，此值至少會保留到所指定的有效位數。 **Decimal**類型會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **decimal**類型。<br /><br /> JDBC **DECIMAL** 類型也會對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **money** 和 **smallmoney** 類型，這兩個是特定的固定有效位數 decimal 類型，分別儲存為 8 個位元組和 4 個位元組。 |
  
## <a name="approximate-numeric-types"></a>近似數值類型

JDBC 近似數數值型別為**REAL**、 **DOUBLE**和**FLOAT**。  
  
| 類型   | 描述                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | JDBC **REAL** 類型具有 7 個位數的有效位數 (單精確度)，並會直接對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **real** 類型。                                                                                                                                     |
| DOUBLE | JDBC **DOUBLE** 類型具有 15 個位數的有效位數 (雙精確度)，並會對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float** 類型。 JDBC **FLOAT**類型是**DOUBLE**的同義字。 由於**FLOAT**和**double**之間可能會產生混淆, 因此偏好**double** 。 |
  
## <a name="datetime-types"></a>日期時間類型

JDBC **TIMESTAMP**類型會對應到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**和**Smalldatetime**類型。 **datetime** 類型會以兩個 4 位元組的整數儲存。 **smalldatetime** 類型會以兩個 2 位元組的小整數來保留相同的資訊 (日期和時間)，但較不精確。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** 類型是固定長度的二進位字串類型。 它不會對應到任何的 JDBC 時間類型:**日期**、**時間**或**時間戳記**。  
  
## <a name="custom-type-mapping"></a>自訂類型對應

JDBC 的自訂類型對應功能，此功能會將 SQLData 介面用於 JDBC 進階類型 (UDT、Struct 等)， 而 JDBC 驅動程式中並未實作此功能。  
  
## <a name="see-also"></a>另請參閱

[了解 JDBC 驅動程式資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
