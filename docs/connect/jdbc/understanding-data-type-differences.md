---
title: 了解資料類型差異 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 105c7d5baa3c2ad7064bf95787975eca2b8c4863
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785613"
---
# <a name="understanding-data-type-differences"></a>了解資料類型差異

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Java 程式設計語言資料類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型之間，存在一些差異。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會透過各種類型的轉換，協助調解這些差異。  

## <a name="character-types"></a>字元類型

JDBC 字元字串資料類型為**CHAR**， **VARCHAR**，並**LONGVARCHAR**。 JDBC 驅動程式提供 JDBC 4.0 API 的支援。 在 JDBC 4.0 中，JDBC 字元字串資料類型也可以**NCHAR**， **NVARCHAR**，並**LONGNVARCHAR**。 這些新的字元字串類型會以 Unicode 格式維護 Java 原生字元類型，並且移除執行任何 ANSI-to-Unicode 或 Unicode-to-ANSI 轉換的需求。  
  
| 類型            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Fixed-length    | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Char**並**nchar**資料類型對應到 JDBC 直接**CHAR**並**NCHAR**型別。 這些是當資料行具有 `SET ANSI_PADDING ON` 時，由伺服器提供填補的固定長度類型。 **nchar** 一定會開啟填補；至於 **char**，當伺服器 char 資料行未開啟填補時，JDBC 驅動程式會新增填補。                                                                                                                                                                                                                                                                                                                                                                                      |
| Variable-length | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Varchar**並**nvarchar**型別會直接對應到 JDBC **VARCHAR**並**NVARCHAR**類型，分別。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 長整數            | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **文字**並**ntext**型別對應到 JDBC **LONGVARCHAR**並**LONGNVARCHAR**類型會分別。 這些是已被取代的類型從[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，因此您應該改用大數值類型**varchar （max)** 或是**nvarchar （max)**，改為。<br /><br /> 使用更新版\<數值類型 > 並[updateObject （int，java.lang.Object）](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md)方法會針對失敗**文字**並**ntext**伺服器資料行。 不過，支援對 **text** 和 **ntext** 伺服器資料行使用 [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) 方法，並搭配指定的字元轉換類型。 |
  
## <a name="binary-string-types"></a>二進位字串類型

JDBC 二進位字串類型為**二進位**， **VARBINARY**，並**LONGVARBINARY**。  
  
| 類型            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Fixed-length    | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **二進位**輸入都會直接對應到 JDBC**二進位**型別。 這是當資料行具有 SET ANSI_PADDING ON 時，會由伺服器提供填補的固定長度類型。 當伺服器 char 資料行未開啟填補時，JDBC 驅動程式會加入填補。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **時間戳記**型別是 JDBC**二進位**具有 8 個位元組的固定長度類型。 |
| Variable-length | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Varbinary**類型會對應到 JDBC **VARBINARY**型別。<br /><br /> **Udt**中輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會對應至為 JDBC **VARBINARY**型別。                                                                                                                                                                                                                                 |
| 長整數            | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **映像**類型會對應到 JDBC **LONGVARBINARY**型別。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，這個類型已淘汰，因此您應該改用大數值類型 **varbinary(max)**。                                                                                                                                                                                           |
  
## <a name="exact-numeric-types"></a>精確數值類型

JDBC 精確數值類型會直接對應到其相對應的 SQL Server 類型。  
  
| 類型     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BIT      | JDBC **BIT** 類型代表可為 0 或 1 的單一位元。 這會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**元**型別。                                                                                                                                                                                                                                                                                                                                       |
| TINYINT  | JDBC **TINYINT** 類型代表單一位元組。 這會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **tinyint**型別。                                                                                                                                                                                                                                                                                                                                                 |
| SMALLINT | JDBC **SMALLINT** 類型代表帶正負號的 16 位元整數。 這會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **smallint**型別。                                                                                                                                                                                                                                                                                                                                     |
| INTEGER  | JDBC **SMALLINT** 類型代表帶正負號的 32 位元整數。 這會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int**型別。                                                                                                                                                                                                                                                                                                                                           |
| bigint   | JDBC **BIGINT** 類型代表帶正負號的 64 位元整數。 這會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bigint**型別。                                                                                                                                                                                                                                                                                                                                         |
| NUMERIC  | JDBC **NUMERIC** 類型代表固定有效位數的十進位值，此值會保留相同的有效位數值。 **數值**類型會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**數值**型別。                                                                                                                                                                                                                                                                   |
| DECIMAL  | JDBC **DECIMAL** 類型代表固定有效位數的十進位值，此值至少會保留到所指定的有效位數。 **十進位**類型會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**十進位**型別。<br /><br /> JDBC **DECIMAL** 類型也會對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **money** 和 **smallmoney** 類型，這兩個是特定的固定有效位數 decimal 類型，分別儲存為 8 個位元組和 4 個位元組。 |
  
## <a name="approximate-numeric-types"></a>近似數值類型

JDBC 近似數值類型為**真正**， **DOUBLE**，並**FLOAT**。  
  
| 類型   | Description                                                                                                                                                                                                                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| real   | JDBC **REAL** 類型具有 7 個位數的有效位數 (單精確度)，並會直接對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **real** 類型。                                                                                                                                     |
| DOUBLE | JDBC **DOUBLE** 類型具有 15 個位數的有效位數 (雙精確度)，並會對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float** 類型。 JDBC**浮點數**型別是的同義字**DOUBLE**。 因為可能會混淆**浮點數**並**雙精度浮點**， **DOUBLE** ，最好使用。 |
  
## <a name="datetime-types"></a>日期時間類型

JDBC**時間戳記**類型會對應至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**並**smalldatetime**型別。 **datetime** 類型會以兩個 4 位元組的整數儲存。 **smalldatetime** 類型會以兩個 2 位元組的小整數來保留相同的資訊 (日期和時間)，但較不精確。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** 類型是固定長度的二進位字串類型。 它不會對應到任何的 JDBC 時間類型：**日期**，**時間**，或**時間戳記**。  
  
## <a name="custom-type-mapping"></a>自訂類型對應

JDBC 的自訂類型對應功能，此功能會將 SQLData 介面用於 JDBC 進階類型 (UDT、Struct 等)， 而 JDBC 驅動程式中並未實作此功能。  
  
## <a name="see-also"></a>另請參閱

[了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
